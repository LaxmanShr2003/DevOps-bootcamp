# Day 6 - DevOps BootCamp

## **Bash Scripting Revision & Python Scripting Basics + AWS Architecture Diagram Practice**

Today was a productive day focusing on scripting and architecture fundamentals.

I started by revising **Bash scripting**, especially the parts I struggled with earlier.

### 🔹 **Bash Scripting Revision**

I revisited the fundamentals:

- **Variables**
    
    Example:
    
    ```bash
    name="Laxman"
    echo "Hello $name"
    
    ```
    
- **Conditions**
    
    ```bash
    if [ $age -ge 18 ]; then
        echo "Adult"
    else
        echo "Minor"
    fi
    
    ```
    
- **Loops**
    
    ```bash
    for user in $(cat users.txt); do
        echo "Processing $user"
    done
    
    ```
    
- **Functions**
    
    ```bash
    greet() {
        echo "Hello from a function!"
    }
    greet
    
    ```
    

### **Practical `awk` Examples**

Extract only usernames from bash script file:

```bash
awk -F: '{print $1}' /etc/passwd

```

Sum values from a column:

```bash
DISK=$(df -h / | awk 'NR==2 {print $3" used / "$2" total ("$5")"}')

```

These revisions helped reinforce the structure and flow of scripts.

---

### 🔹 **Introduction to Python for Automation**

I moved from Bash to **Python scripting**, understanding how Python can automate more complex tasks.

Example: Simple file read automation:

```python
with open("data.txt") as file:
    for line in file:
        print(line.strip())

```

Another small example:

```python
import os
print("Current working directory:", os.getcwd())

```

I also learned how Python scripts can be integrated with AWS tools later using `boto3`.

---

### 🔹 **AWS Architecture Diagram – Hands-on**

I spent time practicing **AWS architecture diagrams**, understanding the typical components:

- VPC
- Subnets
- EC2
- Load Balancers
- S3
- Route 53
- IAM Roles

I practiced making diagrams using lucidchart.

Example architecture I created:

- User → Route 53 → ALB → EC2 Autoscaling Group → RDS
- S3 for static assets
- CloudWatch for monitoring

This helped me visualize how real systems work.