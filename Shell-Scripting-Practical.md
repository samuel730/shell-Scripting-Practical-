# Shell Scripting Project 13: Automated Backup System
## Project Overview

This project demonstrates how to automate a common system administration task using Bash shell scripting in a Linux (WSL Ubuntu) environment.

The script performs automated backups of a specified directory by compressing it into a timestamped archive and storing it in a backup location. It also demonstrates task scheduling using cron jobs for automation.

## Objective

To create a shell script that:

- Backups a directory
- Compresses it into a .tar.gz file
- Stores it in a specified backup location
- Automates the process using cron scheduling

## Tools & Environment
- Linux (Ubuntu via WSL)
- Bash Shell
- tar (file compression utility)
- cron (task scheduler)
### Project Structure
```
/home/username/
│
├── backup.sh
├── projects/        # Source directory (files to backup)
└── /mnt/backups/    # Backup destination
```
## Shell Script
### backup.sh
```
#!/bin/bash

SOURCE_DIR=$1
BACKUP_DIR=$2
TIMESTAMP=$(date +"%Y%m%d%H%M%S")
BACKUP_FILE="$BACKUP_DIR/backup_$TIMESTAMP.tar.gz"

if [ -d "$SOURCE_DIR" ]; then
    tar -czf "$BACKUP_FILE" "$SOURCE_DIR"
    echo "Backup completed: $BACKUP_FILE"
else
    echo "Source directory does not exist."
fi
```

<img width="1250" height="1351" alt="Screenshot 2026-05-25 135400" src="https://github.com/user-attachments/assets/56fcab7f-9fa4-4390-ac69-2001251e4814" />

### How It Works
1. The script accepts two arguments:
- Source directory (what to back up)
- Backup directory (where to store backup)
2. It checks if the source directory exists.
3. If valid:
- It compresses the directory using tar
- Adds a timestamp to prevent overwriting
- Saves it in the backup folder
4. If invalid:
- It displays an error message
## How to Run the Script
### 1. Make script executable
```
chmod +x backup.sh
```

<img width="1208" height="76" alt="image" src="https://github.com/user-attachments/assets/00eff249-c67e-4194-aa38-abdb5910cf61" />

### 2. Create test directories
```
mkdir -p /home/$USER/projects
sudo mkdir -p /mnt/backups
echo "test file" > /home/$USER/projects/file.txt
```

<img width="1240" height="222" alt="image" src="https://github.com/user-attachments/assets/809d18de-c4dc-4aff-b977-d44bda6eefa8" />

### 3. Run script
```
./backup.sh /home/$USER/projects /mnt/backups
```

<img width="1214" height="148" alt="image" src="https://github.com/user-attachments/assets/8a0140a2-33b6-48ae-8f8e-822ba172f2c6" />

### Automating with Cron

Open cron editor:
```
crontab -e
```
Add this line:
```
0 2 * * * /home/$USER/backup.sh /home/$USER/projects /mnt/backups
```
### Cron Schedule Explained
```
0 2 * * *
```
- 0 → minute 0
- 2 → 2 AM
- → every day
- → every month
- → every weekday

👉 Runs backup automatically every day at 2:00 AM

### Verification

Check backup files:
```
ls -l /mnt/backups
```
Expected output:
```
backup_20260525154957.tar.gz
```
## Key Skills Demonstrated
- Bash scripting fundamentals
- File system automation
- Conditional statements in Linux
- File compression using tar
- Task scheduling using cron
- DevOps-style automation workflow
## Conclusion

This project demonstrates how Linux shell scripting can be used to automate system administration tasks. By combining Bash scripting with cron scheduling, repetitive backup tasks are automated efficiently, reducing manual effort and improving system reliability.
