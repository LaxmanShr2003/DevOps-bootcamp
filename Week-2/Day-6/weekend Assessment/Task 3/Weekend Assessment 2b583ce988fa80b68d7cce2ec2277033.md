# Weekend Assessment

Task 3: Write `harden.sh` that applies basic security best practices:

- Disables root login via SSH
- Changes SSH port
- Installs and configures fail2ban
- Disables unused services
- Sets up basic firewall rules (ufw or firewalld)
- Creates a report of what was changed

## **Script:** harden.sh

**Purpose:** Apply basic server hardening on Linux/EC2: SSH hardening, Fail2ban setup, firewall rules, disabling unused services, and generating a report.

---

## **Pre-checks and Setup**

```bash
#!/bin/bash
```

- Declares the script is a bash script.

```bash
if [ $EUID -ne 0 ]; then
    echo "Please run as root: sudo $0"
    exit 1
fi
```

- Checks if the script is run as root.
- `$EUID` = effective user ID. Root = 0.
- If not root → exits with a message.

```bash
GREEN="\e[32m"
YELLOW="\e[33m"
RESET="\e[0m"
```

- Defines **color variables** for output messages.
- Green for success, Yellow for warnings, Reset to normal.

```bash
REPORT="/var/log/harden_report_$(date +%F-%H%M).log"
echo "Server Hardening Report - $(date)" > "$REPORT"
echo "=====================================" >> "$REPORT"
```

- Defines the **report file name** with current date/time.
- Initializes the report file and adds a header.

```bash
log_change() {
    echo "$1" | tee -a "$REPORT"
}
```

- Function to log messages to **screen and report file** simultaneously.
- `$1` is the message passed to the function.

---

## **Detect Default User (EC2 safe)**

```bash
if id ubuntu &>/dev/null; then
    DEFAULT_USER="ubuntu"
elif id ec2-user &>/dev/null; then
    DEFAULT_USER="ec2-user"
else
    DEFAULT_USER=$(whoami)
fi
log_change "Detected default user: $DEFAULT_USER"
```

- Checks if the server has common EC2 default users (`ubuntu` or `ec2-user`).
- If neither exists → uses the current user.
- Logs detected default user.

---

## **Disable Root SSH Login**

```bash
if grep -q "^PermitRootLogin no" /etc/ssh/sshd_config; then
    log_change "Root login is already disabled."
else
    sed -i 's/^#*PermitRootLogin.*/PermitRootLogin no/' /etc/ssh/sshd_config
    log_change "Disabled root login via SSH."
fi
```

- Checks if root login is already disabled.
- If not → modifies `/etc/ssh/sshd_config` to disable root login.
- `sed -i` → edits the file in-place.
- `#*PermitRootLogin.*` → matches both commented/uncommented lines.

---

## **Change SSH Port Safely**

```bash
read -p "Enter new SSH port (default 2222): " SSH_PORT
SSH_PORT=${SSH_PORT:-2222}
```

- Prompts user for a new SSH port.
- If empty → defaults to 2222.

```bash
apt-get update -y >/dev/null 2>&1
apt-get install -y ufw >/dev/null 2>&1

```

- Updates package index.
- Installs UFW (firewall).
- `>/dev/null 2>&1` hides output for clean logging.

```bash
ufw allow "$SSH_PORT"/tcp
log_change "Opened SSH port $SSH_PORT in UFW"
```

- Opens SSH port in UFW **before changing SSH** → prevents lockout.
- Logs action to report.

```bash
if grep -q "^Port" /etc/ssh/sshd_config; then
    sed -i "s/^Port.*/Port $SSH_PORT/" /etc/ssh/sshd_config
else
    echo "Port $SSH_PORT" >> /etc/ssh/sshd_config
fi
log_change "Changed SSH port to $SSH_PORT"
systemctl restart ssh
log_change "SSH service restarted"
```

- Updates `/etc/ssh/sshd_config` with new port.
- Restarts SSH to apply changes.

---

## **Install and Configure Fail2ban**

```bash
apt-get install -y fail2ban >/dev/null 2>&1
log_change "Installed fail2ban"

```

- Installs Fail2ban (protects against brute-force attacks).

```bash
cat > /etc/fail2ban/jail.local <<EOL
[sshd]
enabled = true
port = $SSH_PORT
filter = sshd
logpath = /var/log/auth.log
maxretry = 5
bantime = 3600
EOL
systemctl restart fail2ban
log_change "Configured Fail2ban for SSH"

```

- Configures Fail2ban for SSH:
    - Enabled
    - Custom port
    - Max 5 failed attempts → 1-hour ban
- Restarts Fail2ban.

---

## **Detect and Disable Unused Services**

```bash
log_change "Detecting unused services..."

UNUSED_SERVICES=$(systemctl list-unit-files --type=service \
    | grep enabled \
    | awk '{print $1}' \
    | while read svc; do
        if ! systemctl is-active --quiet "$svc"; then
            echo "$svc"
        fi
    done
)

```

- Finds **enabled but inactive services**.
- `systemctl list-unit-files --type=service` → lists all services.
- `grep enabled` → only those enabled at boot.
- `systemctl is-active` → checks if service is running.
- `UNUSED_SERVICES` stores services that are **enabled but not running**.

```bash
if [ -z "$UNUSED_SERVICES" ]; then
    log_change "No unused services detected"
else
    log_change "Unused services detected:"
    echo "$UNUSED_SERVICES" | tee -a "$REPORT"
    echo -e "${YELLOW}Do you want to disable these services? (y/n)${RESET}"
    read -r confirm
    if [[ "$confirm" == "y" ]]; then
        for service in $UNUSED_SERVICES; do
            systemctl disable --now "$service" 2>/dev/null
            log_change "Disabled: $service"
        done
    else
        log_change "No services were disabled"
    fi
fi

```

- If unused services exist → shows list.
- Asks user before disabling.
- Disables selected services safely.

---

## **Configure UFW Firewall**

```bash
ufw default deny incoming
ufw default allow outgoing
ufw allow 80/tcp
ufw allow 443/tcp
ufw --force enable
ufw reload
log_change "Configured UFW firewall rules"

```

- Blocks all incoming traffic by default.
- Allows outgoing traffic.
- Allows ports: HTTP (80), HTTPS (443).
- Enables firewall forcefully.

---

## **Final Report**

```bash
echo -e "\n${GREEN}=== HARDENING COMPLETE ===${RESET}"
log_change "Root login: disabled"
log_change "SSH port: $SSH_PORT"
log_change "Fail2ban: enabled"
log_change "Firewall: active"
log_change "Report saved at: $REPORT"
cat "$REPORT"

```

- Prints completion message.
- Logs all important changes.
- Displays the full report on screen.

---

# **Summary of Tasks**

| Task | Description |
| --- | --- |
| **Task 1** | Pre-checks: ensure script runs as root, initialize report, set colors. |
| **Task 2** | Detect default EC2 user to prevent lockout. |
| **Task 3** | Disable root login via SSH. |
| **Task 4** | Change SSH port safely (open port in firewall first). |
| **Task 5** | Install and configure Fail2ban for SSH protection. |
| **Task 6** | Detect enabled-but-inactive services and optionally disable them. |
| **Task 7** | Configure UFW firewall: deny incoming, allow outgoing + HTTP/HTTPS. |
| **Task 8** | Generate and display final hardening report. |