# Day - 9 : DevOps Bootcamp Logs

Date : December 2, 2025                                                             Day: Tuesday

        

             Today I learned about two core concepts used heavily in DevOps and cloud environments: **virtualization** and **containerization**. These form the foundation for how modern infrastructure is deployed, scaled, and managed.

---

## **What is Virtualization?**

Virtualization is the practice of separating physical computer resources into multiple **logical** environments.

This means a single physical machine can run multiple **virtual machines (VMs)**, each with:

- its own CPU share
- its own memory
- its own storage
- its own operating system
- its own network configuration

Even though all VMs run on the same hardware, they behave like completely isolated computers.

### **Purpose of Virtualization**

- Better hardware utilization
- Ability to run multiple OS environments
- Easy to replicate servers
- Fast provisioning of systems
- Isolation between workloads (one VM crash doesn’t affect others)
- Cost reduction in data centers

Example:

A single physical server can run a Windows VM, a Linux VM, and a database VM—all at the same time.

---

## **What is Containerization?**

Containerization is the next evolution after virtualization.

Instead of virtualizing the **hardware**, containers virtualize the **operating system**.

A container:

- shares the same OS kernel
- but runs its own isolated environment for applications
- is lightweight compared to VMs
- starts up in seconds

Containers package:

- application
- dependencies
- libraries
- runtime

Into one consistent unit that runs the same everywhere.

### **Why containerization?**

- Faster deployment than VMs
- Lightweight, uses fewer resources
- Ideal for microservices
- Easily portable across environments
- Works perfectly with CI/CD pipelines

Examples of container tools:

- Docker
- Podman

---

# **Summary**

Today I understood the difference between virtualization and containerization.

Virtualization gives full operating systems on top of hardware.

Containerization gives lightweight, fast, isolated application environments on top of a single OS.

These two concepts are at the heart of modern DevOps, cloud infrastructure, and deployment strategies.