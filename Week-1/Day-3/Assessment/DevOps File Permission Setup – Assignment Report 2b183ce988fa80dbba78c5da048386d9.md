# DevOps File Permission Setup – Assignment Report

**Introduction**

This document describes the complete configuration of users, groups, permissions, and security bits (SUID, SGID, Sticky Bit) for /var/www/project in a Linux environment.

**Task 1 : User and Group Creation**

Step 1: Create some users with the help of useradd command with sudo 	
sudo useradd <username>

![image.png](image.png)

```
example:
	sudo useradd -m ram
	sudo useradd -m hari
	sudo useradd -m gita
	sudo useradd -m deploy

```

Step 2: Create some groups with the help of groupadd command with sudo

![image.png](image%201.png)

```
syntax: sudo groupadd <groupname>

example:
	sudo groupadd devteam
	sudo groupadd deployers
	

```

Step 3: Now, Add users to the specific groups with the help of usermod command

![image.png](image%202.png)

```
syntax: sudo usermod -aG <groupname> <username>
example:
	sudo usermod -aG devteam ram
	sudo usermod -aG devteam hari
	sudo usermod -aG devteam gita
	sudo usermod -aG deployers deploy
	

```

**Task 2: Directory and file setup**

Step 1: Create folder named project and make files naming 	source,logs,scripts and shared  inside /var/www/ directory

![image.png](image%203.png)

```
sudo mkdir -p /var/www/project/source
sudo mkdir -p /var/www/project/logs
sudo mkdir -p /var/www/project/scripts
sudo mkdir -p /var/www/project/shared

```

**Task 3: Apply Correct Permissions**

Now, lets see the current permission state of those directories 

![image.png](image%204.png)

According to the diagram shown above, all the new directories are owned by root and part of root group. 

Update the directory permission and ownership

1. Set permission for source/ directory so that:
    
    Only members of devteam can enter and modify /var/www/project/source/ and  
    
    The directory should have correct group ownership and SGID so new
    
    files inherit the group.
    

![image.png](image%205.png)

1. Set permission for logs/ directory so that:
    
    Everyone in devteam can append to logs and no one can modify and delete others logs (use sticky bits)
    
    ![image.png](image%206.png)
    
2. Set permission for *scripts/deploy.sh*  directory so that:
    
    Only the deploy user should be able to execute it and Use SUID so it runs with owner privileges (assume owner is root or deploy)
    
    ![image.png](image%207.png)
    
    1. Set permission for *shared/*  directory so that:
        
        All devteam members can read and write and  use setgid so all new files created belong to devteam group automatically
        
    
    ![image.png](image%208.png)
    

**Task 4: umask and Default Permissions**

Configure the system so that users in devteam have a default umask of 002

when they log in.

Go to  /etc/bashrc  or user-specific profile and add below script. 

![image.png](image%209.png)

This umask helps **users who belong to the devteam group** to have a default `umask 002`, without affecting other users. When any one create any file it will inherit default permission. Specially, umask 002 is default for user and umask 022 is for root in linux