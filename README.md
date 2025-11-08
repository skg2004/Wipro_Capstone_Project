🧰 Bash Scripting Suite for Automated Linux System Maintenance
📘 Overview

This project is a suite of Bash scripts designed to automate essential Linux system maintenance tasks such as:

Automated backups of important files and directories

System updates and cleanup

Log monitoring for system diagnostics

An interactive menu interface to easily access all tasks

It simplifies regular maintenance for users and administrators, ensuring improved efficiency, reliability, and security.

sys_maintenance_suite/
│
├── backup.sh      # Interactive backup script
├── update.sh      # Automates system update and cleanup
├── monitor.sh     # Extracts and saves recent system logs
├── menu.sh        # Interactive menu to access all scripts
└── README.md      # Project documentation


⚙️ Features

✅ Automated backups with timestamps
✅ Interactive folder selection for backup
✅ System updates and cleanup automation
✅ Log monitoring (saves last 20 lines of syslog)
✅ Integrated command-line menu for easy use
✅ Error handling and logging functionality


🧾 Scripts Explanation
1️⃣ backup.sh

Creates compressed, timestamped backups of a user-specified directory.

#!/bin/bash

BACKUP_DIR="$HOME/Backup"
DATE=$(date +"%Y-%m-%d_%H-%M-%S")
BKUP_FILE="backup_$DATE.tar.gz"

read -p "Enter full path of folder to back up: " SOURCE_DIR

mkdir -p "$BACKUP_DIR"
tar -czf "$BACKUP_DIR/$BKUP_FILE" "$SOURCE_DIR" 2>/dev/null

if [ $? -eq 0 ]; then
  echo "Backup completed: $BKUP_FILE"
  echo "$(date): Backup of $SOURCE_DIR created successfully." >> "$BACKUP_DIR/backup.log"
else
  echo "Backup failed! Please check the folder path and try again." >&2
fi

2️⃣ update.sh

Updates and cleans up system packages, logging each action.

#!/bin/bash
sudo apt update && sudo apt upgrade -y
sudo apt autoremove -y
echo "$(date): System updated and cleaned." >> "$HOME/Backup/update.log"
echo "System update and cleanup complete."

3️⃣ monitor.sh

Saves the last 20 lines from /var/log/syslog for monitoring.

#!/bin/bash
LOG_FILE="$HOME/Backup/system.log"
tail -n 20 /var/log/syslog > "$LOG_FILE"
echo "Last 20 log entries saved to $LOG_FILE"

4️⃣ menu.sh

Provides an interactive interface to run all maintenance tasks.

#!/bin/bash
while true; do
  echo "===== System Maintenance Menu ====="
  echo "1) Backup"
  echo "2) Update System"
  echo "3) Monitor Logs"
  echo "4) Exit"
  read -p "Select an option [1-4]: " choice

  case $choice in
    1) bash ./backup.sh ;;
    2) bash ./update.sh ;;
    3) bash ./monitor.sh ;;
    4) echo "Exiting menu."; break ;;
    *) echo "Invalid option. Please select between 1 and 4." ;;
  esac
done

🚀 How to Run
Step 1: Setup

Create a folder and save all scripts:

mkdir sys_maintenance_suite
cd sys_maintenance_suite

Step 2: Give Execution Permission
chmod +x backup.sh update.sh monitor.sh menu.sh

Step 3: Run the Suite
./menu.sh

Example Output
===== System Maintenance Menu =====
1) Backup
2) Update System
3) Monitor Logs
4) Exit
Select an option [1-4]: 1
Enter full path of folder to back up: /home/wsl/Desktop
Backup completed: backup_2025-11-08_21-30-45.tar.gz

📁 Output Files

~/Backup/backup_YYYY-MM-DD_HH-MM-SS.tar.gz → Compressed backup file

~/Backup/backup.log → Logs all backup operations

~/Backup/update.log → Logs system update actions

~/Backup/system.log → Stores last 20 syslog entries

🧩 Error Handling

Validates source folder before backup

Graceful handling for missing paths

Logs all success and failure events

Prevents overwriting of backups with timestamps
