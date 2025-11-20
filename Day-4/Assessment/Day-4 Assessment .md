# Day-4: Assessment

**Assignment 3: A DevOps Engineer wants to track the top CPU-consuming process.**Tasks: Write a script that:

- Identifies the PID using the most CPU
- **Logs its PID, process name, and CPU usage to `cpu_report.txt`**

![image.png](image.png)

Output:

![image.png](image%201.png)

# **Breakdown of Each Part**

## **1. `ps`**

Shows running processes in Linux.

---

## **2. `e`**

Means **show all processes** running on the system.

---

## **3. `o pid,user,comm,%cpu`**

This selects **specific columns** to display:

| Option | Meaning |
| --- | --- |
| **pid** | Process ID |
| **user** | Owner of the process |
| **comm** | Command/program name running |
| **%cpu** | CPU usage percentage |

So output will show columns like:

```
PID   USER   COMMAND   %CPU

```

---

## **4. `-sort=-%cpu`**

Sorts the process list by **CPU usage descending** (highest first).

The minus `-` means *descending order*.

---

## **5. `| head -n 2`**

Pipes the output to `head` and shows only **first 2 lines**.

- Line 1 → header
- Line 2 → **most CPU-consuming process**

---

## **6. `> cpu_report.txt`**

Redirects the output into a file named **cpu_report.txt**.

So the result is saved instead of printed.

---

## **7. `cat cpu_report.txt`**

Displays the contents of the file.