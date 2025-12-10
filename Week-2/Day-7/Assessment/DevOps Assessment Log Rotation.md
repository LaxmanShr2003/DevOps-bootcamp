# DevOps Assessment

**Log Rotation and Cleanup Description**

You need to implement a log rotation system on your server where logs older than 30 days are deleted, and a new log file is created every day. This should be applied to application logs in `/var/log/app_logs/`.

**Requirements**:

- Create a script that checks for log files older than 30 days and removes them.
- Ensure that a new log file is created every day with a timestamp.
- Ensure that logs are compressed for archival.

## **Overview**

This document describes the setup of a custom **log rotation and cleanup system** for application logs stored in:

```
/var/log/app_logs/
```

The solution includes:

- Automatic daily log creation
- Compression of old logs
- Deletion of logs older than 30 days
- Cron automation
- Logging of rotation activity

This setup ensures optimized disk usage, clean log history, and maintainable log management.

---

# **Directory Structure**

All application logs will be stored under:

```
/var/log/app_logs/
```

Example structure:

```
/var/log/app_logs/
│── application-2025-11-27.log
│── application-2025-11-26.log.gz
│── rotation.log           (cron output)

```

---

# **Log Rotation Script**

### **Location:**

```
/usr/local/bin/log_rotator.sh
```

### **Purpose:**

This script:

- Removes log files older than 30 days
- Compresses logs from previous days
- Creates a new log file daily
- Prints user-friendly status messages

---

## **Script Code**

```bash
#!/bin/bash

LOG_DIR="/var/log/app_logs"
TODAY=$(date +"%Y-%m-%d")
TODAY_LOG="$LOG_DIR/application-$TODAY.log"

echo "==============================================="
echo "   Log Rotation Started: $(date)"
echo "   Log Directory: $LOG_DIR"
echo "==============================================="

# Create log directory if missing
mkdir -p "$LOG_DIR"
echo "[OK] Ensured log directory exists."

# 1. Delete logs older than 30 days
find "$LOG_DIR" -type f -mtime +30 -name "*.log" -exec rm -f {} \;
find "$LOG_DIR" -type f -mtime +30 -name "*.gz" -exec rm -f {} \;
echo "[OK] Old logs (older than 30 days) deleted."

# 2. Compress old logs except today's
find "$LOG_DIR" -type f -name "*.log" ! -name "application-$TODAY.log" -exec gzip -f {} \;
echo "[OK] Previous log files compressed."

# 3. Create today's log file
if [[ ! -f "$TODAY_LOG" ]]; then
    touch "$TODAY_LOG"
    echo "[OK] Created today's log file: $TODAY_LOG"
else
    echo "[INFO] Today's log already exists: $TODAY_LOG"
fi

echo "==============================================="
echo "   Log Rotation Completed Successfully"
echo "==============================================="

```

### Make it executable:

```
sudo chmod +x /usr/local/bin/log_rotator.sh
```

---

# ⏱️ **Cron Job Setup**

### Edit the root cron:

```
sudo crontab -e
```

### Add the following entry:

```
0 0 * * * /usr/local/bin/log_rotator.sh >> /var/log/app_logs/rotation.log 2>&1
```

### What this does:

- Runs the script **every day at midnight**
- Saves both output and error logs to:

```
/var/log/app_logs/rotation.log
```

---

# **How It Works Internally**

| Step | Description |
| --- | --- |
| **1. Directory validation** | Ensures `/var/log/app_logs/` exists |
| **2. Daily log creation** | Creates `application-YYYY-MM-DD.log` |
| **3. Compression** | Compresses all older `.log` files to `.gz` |
| **4. Cleanup** | Deletes all logs older than **30 days** |
| **5. Logging** | Writes script output to `rotation.log` via cron |

---

# 🧪 **Testing the Setup**

### Test script manually:

```
sudo /usr/local/bin/log_rotator.sh
```

### Verify daily log:

```
ls -l /var/log/app_logs/
```

### Check rotation logs:

```
cat /var/log/app_logs/rotation.log
```

---

# **Permissions & Security**

- Script should be executable:
    
    ```
    chmod +x /usr/local/bin/log_rotator.sh
    ```
    
- Log directory must be writable by the application or root:
    
    ```
    sudo chown -R root:root /var/log/app_logs
    sudo chmod 755 /var/log/app_logs
    ```