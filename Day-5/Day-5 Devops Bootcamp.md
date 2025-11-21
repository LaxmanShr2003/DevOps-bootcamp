# Day-5: Devops Bootcamp

Date: 21st Nov 2025

**Revision Bash Scripting**

**Today I revised several important Bash scripting concepts.**

Mostly focused on automation tools like cron, file metadata behavior, and powerful text-processing commands like `sed` and `awk`.

---

### **How Cron Works**

I learned how the Linux **crontab** system schedules tasks automatically.

- Cron runs commands at specific times or intervals.
- Each cron job follows a 5-field format:
    
    `minute hour day month weekday`
    

Example: run a script every day at 2 AM:

```
0 2 * * * /home/user/backup.sh

```

I also learned how to open and edit crontab:

```
crontab -e

```

And list existing cron jobs:

```
crontab -l

```

---

### **Tool to Learn Crontab (Cron Guru)**

I used **crontab.guru**, which is a very helpful tool.

It explains cron expressions and shows in plain English what the schedule means.

Example:

Typing `*/5 * * * *` in crontab.guru says:

“Every 5 minutes.”

This helped me understand cron timing patterns quickly.

---

### **How `touch` Works**

I revisited how the `touch` command behaves.

- If the file **does not exist**, it creates it.
- If the file **already exists**, `touch` **updates the timestamp** (modification time).

Example:

```
touch notes.txt
ls -l notes.txt

```

This made me remember how Linux file metadata works (mtime, atime, ctime).

---

### **Text Processing Tools: sed and awk**

### **sed (Stream Editor)**

Used for finding, replacing, and editing text in streams or files.

Examples:

Replace “apple” with “orange”:

```
sed 's/apple/orange/' fruits.txt

```

Delete a specific line (line 3):

```
sed '3d' file.txt

```

### **awk**

A powerful pattern-scanning and processing tool.

Examples:

Print the first column:

```
awk '{print $1}' file.txt

```

Print only lines where the value in column 3 > 50:

```
awk '$3 > 50' data.txt

```

I learned that `awk` is very useful for logs, CSV files, system stats, etc.

---

### **Summary**

Today I revised cron jobs, learned how crontab works using Cron Guru and reviewed how `touch` command updates file timestamps, and practiced text-processing and manupulation commands like `sed` and `awk`. These tools are essential for automation and log processing in DevOps.