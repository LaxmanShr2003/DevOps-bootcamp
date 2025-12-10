# Day 7: DevOps BootCamp

# **Git Basics Learning Log**

Today I focused on learning the basic concepts of **Git** and practiced how version control works. I mainly worked on understanding the workflow of adding files, committing changes, pushing code, and creating branches.

---

### **1. What Git Is**

- Git is a version control system used to track file changes.
- It allows multiple people to work on the same project without overwriting each other’s work.
- Helps roll back to previous versions if something breaks.

---

## **2. Basic Git Commands I Practiced**

```bash
git init        # initialize a repository
git status      # check what changed
git add .       # move changes to staging area
git commit -m "message"   # save the snapshot

```

I practiced making small changes in files, checking status, adding, and committing.

---

## **3. Connecting to GitHub (Basics Only)**

- Created a repository on GitHub
- Linked my local repo with:

```bash
git remote add origin <repo-url>
git push -u origin main
```

This helped me understand how code moves from my local machine to GitHub repository.

---

## **4. Git Branching**

Today I also learned how branches work.

### **Why branches?**

- To work on features without affecting the main code.
- Useful when testing ideas.
- Helps keep the project clean and organized.

### **Commands I learned:**

Create a new branch:

```bash
git branch feature1
```

Switch to that branch:

```bash
git checkout feature1

```

Create + switch (shortcut):

```bash
git checkout -b feature/login

```

Go back to main:

```bash
git checkout main

```

After finishing the work:

```bash
git merge feature/login

```

This gave me a basic idea of how developers work on separate branches and merge changes later.

---

# **Summary**

Today I learned the fundamentals of Git: initialization, tracking changes, committing, pushing to GitHub, and basic branching.