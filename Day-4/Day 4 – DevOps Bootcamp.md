# Day 4 – DevOps Bootcamp

**Today learned Linux shell fundamentals.**

The difference between interactive and non-interactive shells and practiced identifying when each type is used.

### **Interactive vs Non-Interactive Shells**

- **Interactive shell:** I type commands directly and get output.
    
    Example: opening a terminal and typing:
    
    `ls -l`
    
- **Non-interactive shell:** Used by scripts, runs without user input.
    
    Example:
    
    `bash script.sh`
    

This helped me understand why some variables appear in terminal but not inside scripts.

**Learned about Linux architecture.**

Reviewed how the hardware, kernel, shell, and application layers work together. This helped me understand how commands travel through the system.

I reviewed the main layers:

1. Hardware
2. Kernel
3. Shell
4. Applications

Understanding this clarified how commands move from user → shell → kernel → hardware.

### **Subshells**

I learned that parentheses create subshells.

Example:

```
(name="Laxman"; echo $name)   # inside subshell
echo $name                    # outside, not available

```

This showed me that subshell changes don’t affect the parent shell.

### **Variables (Local & Global)**

- **Local variable:** Only available in the current shell.
    
    `x=10`
    
- **Global variable:** Available in the shell and subshells.
    
    `export x=10`
    

I practiced checking inheritance using:

```
echo $x
bash -c 'echo $x'

```

### **Environment Variables**

I explored common variables like:

`PATH`, `HOME`, `USER`, `SHELL`.

Examples I used:

```
printenv PATH
export MYNAME="Laxman"

```

### **Quotations**

I practiced how different quotes behave:

- `' '` → literal
- `" "` → expands variables
- `` `` or `$()` → run a command

Example:

```
echo "Today is $(date)"
echo 'Today is $(date)'   # literal

```

### **Special Characters**

Revised commonly used ones:

- wildcard
- `?` single character match
- `|` pipe
- `>` redirect output
- `&&` run only if previous command succeeds

Example:

```
ls *.txt
cat file.txt | grep "error"

```

**Practiced arithmetic operations.**

Used `$(( ))` for addition, incrementing variables, and simple expressions.

- **Worked on flow control.**

Revised:

– if / else conditions

I practiced writing small scripts using these.

**Practiced file operations in shell scripts.**

Read files line by line, used redirection, and checked file/directory existence.

### **Summary**

Overall, today I strengthened my Linux fundamentals by practicing shell behavior, variables, subshells, environment variables, quoting rules, special characters, flow control, arithmetic operations, and file handling. Using small practical examples made the concepts much clearer.