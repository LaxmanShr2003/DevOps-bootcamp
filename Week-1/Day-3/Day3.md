# Day 3 – DevOps Bootcamp

## 1. Revision of Linux Learnings
Today I revised the core Linux fundamentals covered earlier, including:
- Basic navigation commands  
- File and directory operations  
- Process management  
- Networking commands  
- Package management  
- File permissions and ownership  

This revision helped strengthen my understanding of how Linux works and why it is essential in DevOps.

---

## 2. Hands-on Practice: User & Permission Management
I practiced various real Linux operations related to users, groups, and file permissions:

### **User & Group Management**
- Creating users and groups  
- Adding users to groups  
- Checking user information (`id`, `whoami`, `groups`)  
- Managing ownership with `chown` and `chgrp`  

### **Permissions**
- Understanding read (`r`), write (`w`), execute (`x`) permissions  
- Changing permissions using `chmod`  
- Working with numeric and symbolic modes  

---

## 3. Learned: SUID, SGID & Sticky Bit

### **SUID (Set User ID)**
- Executable file runs with **file owner's permissions**.  
- Useful for commands that require elevated privileges.  
  

### **SGID (Set Group ID)**
- Files: runs with **group permissions**.  
- Directories: new files inherit the **group of the directory**.  
  

### **Sticky Bit**
- Applied on directories like `/tmp`.  
- Only the **file owner** can delete or modify files inside the directory.  
 

These special permission bits are essential for secure file sharing, collaborative directories, and privileged command execution.

---

## Summary – What I Learned Today
Today I revised core Linux concepts and practiced hands-on user and permission management. I also learned about advanced permission controls such as **SUID**, **SGID**, and the **Sticky Bit**, which improve security and manage shared environments in Linux systems.

---
