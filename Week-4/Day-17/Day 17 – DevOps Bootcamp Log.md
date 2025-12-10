# Day 17 – DevOps Bootcamp Log

Today’s session focused on Docker build cache, AWS CLI, and understanding file paths inside Docker containers. These topics helped me understand how container builds are optimized and how cloud resources can be managed efficiently.

---

## **1. Docker Build Cache**

I learned how Docker caches intermediate steps during a build to speed up subsequent builds.

- Each command in a Dockerfile creates a layer.
- Docker reuses layers from previous builds if the command and context haven’t changed.
- This makes builds faster and more efficient.

### **Example**

```docker
FROM node:18
WORKDIR /app
COPY package.json .
RUN npm install
COPY . .
CMD ["npm", "start"]

```

- If `package.json` hasn’t changed, Docker uses the cached `npm install` layer instead of running it again.
- Useful for development and CI/CD pipelines.

---

## **2. Understanding Paths in Docker**

While working with Docker, I learned why paths like `/app` vs `app/` are important:

- `/app` → Absolute path inside the container
    - The container will always use this exact location regardless of the current directory.
    - Example: `WORKDIR /app` ensures all subsequent commands run in `/app`.
- `app/` → Relative path
    - Refers to a directory relative to the **current working directory**.
    - Often used when copying files from the host into the container:
        
        ```docker
        COPY app/ /app
        
        ```
        
- Understanding these paths ensures files are placed correctly and prevents build errors or missing files.

Key takeaway: **File paths are critical in Docker** because the container has its own filesystem separate from the host. Choosing the right absolute or relative path ensures proper image builds and consistent runtime behavior.

---

## **3. AWS CLI Demonstration**

The instructor demonstrated **AWS CLI (Command Line Interface)**:

- Using CLI to manage AWS services without logging into the console.
- Commands shown:
    - `aws s3 ls` – List S3 buckets
    - `aws ec2 describe-instances` – List EC2 instances

Key takeaway: AWS CLI allows **automation** and **scripting** of cloud operations, which is critical for DevOps pipelines.

---

## **4. Summary**

Today I learned:

- How Docker build cache optimizes image builds
- How to correctly use absolute (`/app`) vs relative (`app/`) paths in Dockerfiles
- How AWS CLI can manage cloud resources efficiently

This session helped me connect containerization, file system understanding, and cloud management, which are core skills in DevOps workflows.