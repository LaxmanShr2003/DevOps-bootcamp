# Day-20-DevOps Bootcamp Logs

# **AWS S3 & Infrastructure as Code**

Today’s session was focused on **Amazon S3**, its storage classes, lifecycle management, secure access methods, and an introduction to **CloudFormation** through a demo template. This helped me understand how storage and infrastructure automation work together in real cloud environments.

---

## **1. Amazon S3 Overview & Scope**

I learned that **Amazon S3 (Simple Storage Service)** is an object storage service used for storing and retrieving any amount of data.

Its scope is **global**, but buckets are created in a **specific region**.

Key points:

- Highly durable and scalable
- Used for backups, static websites, logs, and data storage
- Access controlled using IAM policies and bucket policies

---

## **2. S3 Storage Classes**

I studied different S3 storage classes and when to use them:

- **S3 Standard** – Frequently accessed data
- **S3 Intelligent-Tiering** – Automatically moves data based on access patterns
- **S3 Standard-IA (Infrequent Access)** – Data accessed less often
- **S3 One Zone-IA** – Lower cost, single AZ
- **S3 Glacier Instant Retrieval** – Rarely accessed, instant access
- **S3 Glacier Flexible Retrieval** – Archival data
- **S3 Glacier Deep Archive** – Long-term archival at lowest cost

---

## **3. S3 Storage Class Transition**

I learned how S3 allows **automatic transitions** between storage classes using lifecycle rules.

Example transitions:

- Standard → Standard-IA after 30 days
- Standard-IA → Glacier after 90 days
- Glacier → Deep Archive after 180 days

This helps reduce storage cost without manual intervention.

---

## **4. Lifecycle Management**

Lifecycle rules allow automation of:

- Transitioning objects between storage classes
- Expiring (deleting) old objects
- Managing object versions

Use cases:

- Log retention
- Backup cleanup
- Archival strategies

---

## **5. Pre-Signed URLs**

I learned about **pre-signed URLs**, which provide **temporary access** to private S3 objects.

Key benefits:

- Secure file sharing
- Time-limited access
- No need to make bucket public

Common use cases:

- Download/upload links for users
- Secure media access

---

## **6. CloudFormation Discussion (Demo Template)**

Today’s session also included a **CloudFormation demo**, where we discussed how templates are used to define infrastructure as code.

Key takeaways:

- Infrastructure is defined using YAML/JSON templates
- Resources like S3 buckets, EC2, IAM can be automated
- Enables repeatable, version-controlled deployments
- Reduces manual configuration errors

---

## **Summary**

Today I gained a solid understanding of:

- Amazon S3 and its storage scope
- Different S3 storage classes and cost optimization
- Lifecycle rules and storage class transitions
- Secure access using pre-signed URLs
- Basic CloudFormation concepts through a demo

This session connected **cloud storage management** with **infrastructure automation**, which is essential for scalable DevOps workflows.

[Day-20-Assessment](https://www.notion.so/Day-20-Assessment-2c883ce988fa804c8d0be2ea583f5be7?pvs=21)