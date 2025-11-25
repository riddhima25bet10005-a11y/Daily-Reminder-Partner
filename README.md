# Daily Reminder Partner
A simple and effective desktop application built with Python and Tkinter that helps you set daily reminders and get pop-up notifications at the specified times.
# Description
Daily Reminder Partner is a lightweight desktop application that allows you to set reminders for your daily tasks. When the set time arrives, you'll receive a pop-up notification with your reminder message. Your reminders are automatically saved and persist between application sessions.
# Features
•	Easy Reminder Setup: Quickly add reminders with time and message
•	Persistent Storage: Reminders are saved automatically in a JSON file
•	Simple Interface: Clean and user-friendly Tkinter GUI
•	24-hour Format: Set reminders using 24-hour time format (HH:MM)
•	Reminder Management: View and delete reminders as needed
•	Background Monitoring: Runs in background to check for due reminders
•	Cross-Platform: Works on Windows, macOS, and Linux
# Installation
# Prerequisites
•	Python 3.6 or higher
•	Tkinter (usually comes with Python)
# Steps
1.	Clone or download this repository
2.	Ensure you have Python installed on your system
3.	No additional packages required - uses only standard Python libraries
# How to Use
Running the Application
bash
python daily_reminder.py
# Setting a Reminder
1.	Enter the time in 24-hour format (e.g., "14:30" for 2:30 PM)
2.	Type your reminder message
3.	Click "Add Reminder"
4.	The reminder will appear in your list
# Managing Reminders
•	View: All reminders are displayed in the list
•	Delete: Select a reminder and click "Delete Selected"
•	Notifications: When reminder time matches current time, a pop-up appears
# Example
•	Time: 09:00
•	Message: Team standup meeting
•	Result: At 9:00 AM, you'll get a pop-up: "Time: 09:00 - Message: Team standup meeting"
# File Structure
text
daily_reminder_partner/
├── daily_reminder.py    # Main application file
├── reminders.json       # Auto-generated reminders storage
└── README.md           # This file
# Technical Details
# Dependencies
•	tkinter - GUI framework
•	threading - Background reminder checking
•	datetime - Time handling
•	json - Data persistence
•	time - Sleep intervals
•	os - File operations
# Data Storage
Reminders are stored in reminders.json in the same directory as the script:
json
[
  {"time": "09:00", "message": "Morning meeting"},
  {"time": "13:30", "message": "Lunch with team"}
]
# Limitations
•	Only supports 24-hour time format
•	Reminders trigger only once per day
•	No recurring reminder options
•	Basic GUI interface
•	No sound notifications (only visual pop-ups)
# Troubleshooting
Application won't start:
•	Ensure Python is installed and added to PATH
•	Verify all required files are in the same directory
Reminders not triggering:
•	Keep the application running in background
•	Check system time format matches 24-hour
Reminders lost:
•	Don't delete reminders.json file
•	Application creates backup automatically
# Future Enhancements
Potential improvements for this application:
•	Recurring reminders (daily, weekly)
•	Sound notifications
•	Categorization of reminders
•	Snooze functionality
•	System tray integration
•	Email/SMS notifications
# Development
# Code Structure
•	DailyReminderApp class handles the main application
•	GUI built with Tkinter widgets
•	Background thread monitors reminder times
•	JSON file used for data persistence
# Modifying the Code
The code is well-commented and modular. Key sections:
•	create_widgets() - GUI setup
•	add_reminder() - Add new reminders
•	check_reminders() - Background monitoring
•	save_reminders()/load_reminders() - Data persistence
________________________________________
# Never forget important tasks again! 
For issues or suggestions, please check the code comments or create an issue in the repository.
 

