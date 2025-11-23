# Daily-Reminder-Partner
This is a basic aaplication in which you can set a reminder and get a pop up of your task on that time 
import tkinter as tk
from tkinter import messagebox, ttk
import time
import threading
from datetime import datetime
import json
import os

class DailyReminderApp:
    def __init__(self, root):
        self.root = root
        self.root.title("Daily Reminder Partner")
        self.reminders = []
        self.load_reminders()
        
        
        self.create_widgets()
        
        self.running = True
        self.thread = threading.Thread(target=self.check_reminders, daemon=True)
        self.thread.start()
        
        self.root.protocol("WM_DELETE_WINDOW", self.on_close)

    def create_widgets(self):
        
        main_frame = ttk.Frame(self.root, padding="10")
        main_frame.grid(row=0, column=0, sticky=(tk.W, tk.E, tk.N, tk.S))

        
        ttk.Label(main_frame, text="Time (HH:MM):").grid(row=0, column=0, sticky=tk.W, pady=5)
        self.time_entry = ttk.Entry(main_frame, width=15)
        self.time_entry.grid(row=0, column=1, pady=5, padx=5)

        
        ttk.Label(main_frame, text="Message:").grid(row=1, column=0, sticky=tk.W, pady=5)
        self.message_entry = ttk.Entry(main_frame, width=30)
        self.message_entry.grid(row=1, column=1, pady=5, padx=5)

        
        ttk.Button(main_frame, text="Add Reminder", command=self.add_reminder).grid(row=2, column=0, columnspan=2, pady=10)

        
        self.reminder_list = tk.Listbox(main_frame, width=50, height=15)
        self.reminder_list.grid(row=3, column=0, columnspan=2, pady=10)
        self.update_reminder_list()

        
        ttk.Button(main_frame, text="Delete Selected", command=self.delete_reminder).grid(row=4, column=0, columnspan=2, pady=5)

    def add_reminder(self):
        time_str = self.time_entry.get()
        message = self.message_entry.get()

        try:
            
            datetime.strptime(time_str, "%H:%M")
        except ValueError:
            messagebox.showerror("Error", "Invalid time format! Use HH:MM (24-hour format)")
            return

        if not message:
            messagebox.showerror("Error", "Message cannot be empty!")
            return

        self.reminders.append({"time": time_str, "message": message})
        self.save_reminders()
        self.update_reminder_list()
        self.time_entry.delete(0, tk.END)
        self.message_entry.delete(0, tk.END)

    def delete_reminder(self):
        selected = self.reminder_list.curselection()
        if selected:
            index = selected[0]
            del self.reminders[index]
            self.save_reminders()
            self.update_reminder_list()

    def update_reminder_list(self):
        self.reminder_list.delete(0, tk.END)
        for reminder in self.reminders:
            self.reminder_list.insert(tk.END, f"{reminder['time']} - {reminder['message']}")

    def check_reminders(self):
        while self.running:
            now = datetime.now().strftime("%H:%M")
            for reminder in self.reminders:
                if reminder["time"] == now:
                    self.show_reminder(reminder["message"])
                    
                    time.sleep(61)  
            time.sleep(30)  

    def show_reminder(self, message):
        
        self.root.after(0, lambda: messagebox.showinfo("Reminder!", f"Time: {datetime.now().strftime('%H:%M')}\nMessage: {message}"))

    def load_reminders(self):
        if os.path.exists("reminders.json"):
            with open("reminders.json", "r") as f:
                self.reminders = json.load(f)

    def save_reminders(self):
        with open("reminders.json", "w") as f:
            json.dump(self.reminders, f)

    def on_close(self):
        self.running = False
        self.root.destroy()

if __name__ == "__main__":
    root = tk.Tk()
    app = DailyReminderApp(root)
    root.mainloop()
