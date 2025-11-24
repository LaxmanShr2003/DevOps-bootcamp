# Weekend Assignment

Task 2: Your teammate always asks “What is the IP of this server?” so please create a bash script as

which shows only the private and public IP in a pretty way.

# **Task 2 — Show Private & Public IP**

**Purpose:** Quickly display the server’s private and public IP addresses in a clean, colored format.

---

## **Script: myip.sh**

```bash
#!/bin/bash
```

- Declares this as a bash script.

```bash
# Colors (optional)
GREEN="\e[32m"
CYAN="\e[36m"
YELLOW="\e[33m"
RESET="\e[0m"

```

- Defines **ANSI color codes** to make output more readable.
- `RESET` returns terminal text to normal color.

---

### **Step 1 — Get Private IP**

```bash
PRIVATE_IP=$(ip addr show | awk '/inet / && $2 !~ /^127/ && $NF !~ /docker/ {print $2}' | cut -d/ -f1 | head -n 1)

```

- `ip addr show` → lists all network interfaces and IP addresses.
- `awk '/inet / && $2 !~ /^127/ && $NF !~ /docker/ {print $2}'`
    - Filters lines containing `inet` (IPv4 addresses).
    - Excludes **loopback** (`127.*`) and **docker interfaces**.
    - Prints the IP with subnet (e.g., `192.168.1.10/24`).
- `cut -d/ -f1` → removes subnet, keeps only IP (`192.168.1.10`).
- `head -n 1` → in case multiple interfaces, take the first one.

✅ Result stored in variable `PRIVATE_IP`.

---

### **Step 2 — Get Public IP**

```bash
PUBLIC_IP=$(curl -s ifconfig.me)

```

- Uses `curl` to query `ifconfig.me` to get the **public IP**.
- `s` → silent mode (no progress or errors).
- Result stored in `PUBLIC_IP`.

---

### **Step 3 — Display IPs in a Pretty Format**

```bash
echo -e "${GREEN}=============================="
echo -e "        SERVER IP INFO"
echo -e "==============================${RESET}"

```

- Prints a **green colored header** for clarity.

```bash
echo -e "${CYAN}Private IP :${RESET} $PRIVATE_IP"
echo -e "${YELLOW}Public  IP :${RESET}  $PUBLIC_IP"

```

- Prints **Private IP** in cyan.
- Prints **Public IP** in yellow.
- `${RESET}` ensures text after it is normal color.
- Prints a **green footer line** for visual separation.

---

---

### **Example Output**

![image.png](image.png)