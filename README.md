🧰 Bash Scripting Suite for Automated Linux System Maintenance
📘 Overview

This project is a suite of Bash scripts designed to automate essential Linux system maintenance tasks such as:

Automated backups of important files and directories

System updates and cleanup

Log monitoring for system diagnostics

An interactive menu interface to easily access all tasks

It simplifies regular maintenance for users and administrators, ensuring improved efficiency, reliability, and security.

## 🗂️ Project Structure
sys_maintenance_suite/
│
├── backup.sh # Interactive backup script
├── update.sh # Automates system update and cleanup
├── monitor.sh # Extracts and saves recent system logs
├── menu.sh # Interactive menu to access all scripts
└── README.md # Project documentation



---

## 🧩 Scripts Overview

### 1. **backup.sh**
- Prompts the user to input a directory path.
- Creates a compressed `.tar.gz` backup with timestamp.
- Stores backups in `$HOME/Backup` directory.
- Logs backup activity in `backup.log`.

### 2. **update.sh**
- Updates and upgrades system packages automatically.
- Cleans unused packages and cache to free disk space.
- Records update activity in `update.log`.

### 3. **monitor.sh**
- Monitors system logs (like `/var/log/syslog`).
- Extracts and saves logs for the current date.
- Alerts when specific keywords (like “error” or “failed”) are found.

### 4. **menu.sh**
- Provides an interactive menu with options:
  - Run Backup
  - Perform System Update
  - View Logs
  - Exit
- Executes respective scripts based on user choice.

---

## ⚙️ How to Run

1. **Make all scripts executable:**
   ```bash
   chmod +x *.sh

🧾 Log Files

backup.log: Records all successful backups.

update.log: Records all system update activities.

monitor.log: Contains extracted or filtered system logs.
