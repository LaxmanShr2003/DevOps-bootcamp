# Day 11 – DevOps Bootcamp Logs

**Topic:** Docker

**Duration:** Day 11 (2-day interval)

---

## **1. Overview**

On Day 11, I continued learning Docker, focusing on essential containerization concepts used in real-world development. I explored how Docker handles command history, volume mapping, Dockerfile creation, and Docker Compose for multi-service orchestration.

---

## **2. What I Learned**

### **🔹 1. Searching Command History**

- I learned that in Linux terminal and Docker workflows, pressing **`Ctrl + R`** allows me to *search previously used commands interactively*.
- This is especially useful when re-running long Docker commands such as:
    - `docker run ...`
    - `docker build ...`
    - `docker compose up`

---

### **🔹 2. Volume Mapping**

- Docker volumes are used to **persist data** even after containers are removed.
- Volume mapping helps store files on the host machine instead of inside the container.

**Example:**

```bash
docker run -v myvolume:/var/www/html nginx

```

**Key points learned:**

- Volumes help retain logs, database data, and server configurations.
- Bind mounts allow linking local folders to containers during development.

---

### **🔹 3. Dockerfile**

- A Dockerfile is a script containing instructions to build a custom Docker image.

**Basic Dockerfile example:**

```docker
FROM nginx
WORKDIR /app
COPY package.json .
RUN npm install
COPY . .
CMD ["npm", "start"]

```

**Concepts learned:**

- `FROM` sets the base image
- `COPY` copies files into container
- `RUN` executes commands during image build
- `CMD` defines default container start command

---

### **🔹 4. Docker Compose**

- Docker Compose is used to run **multi-container applications** using a YAML file.

**Example:**

```yaml
services:
  app:
    image: nginx
    volumes:
      - nginx_html:/usr/share/nginx/html
    ports:
      - "81:80"

```

**What I practiced:**

- Running multiple services together using `docker compose up`
- Defining ports, networks, volumes inside compose file
- Understanding how services communicate internally

---

## **3. Summary**

Day 11 helped strengthen my understanding of Docker fundamentals. I learned how to manage persistent data using volumes, create custom images using Dockerfiles, and orchestrate multi-container applications using Docker Compose. I also practiced using terminal shortcuts like **Ctrl + R** to improve workflow efficiency.

[Assessment: **Data Persistence in Containers**](https://www.notion.so/Assessment-Data-Persistence-in-Containers-2c083ce988fa802abae3ed4412e428ad?pvs=21)