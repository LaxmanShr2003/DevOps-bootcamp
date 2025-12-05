# Assessment: Data Persistence in Containers

## **Objective**

To understand how Docker handles data inside containers, how data behaves after stopping/removing containers, and how to properly persist data using **Docker volumes**.

This assessment focuses on:

1. Running an NGINX container
2. Modifying website content
3. Checking persistence after restart
4. Checking persistence after removing the container
5. Using Docker volumes to achieve real persistence

---

# **1. Pull and Run NGINX Container**

### **Step 1: Pull the NGINX Image**

```bash
docker pull nginx

```

### **Step 2: Run the Container**

```bash
docker run --name mynginx -p 8080:80 -d nginx

```

### **Step 3: View the Default NGINX Page**

Open browser and visit:

```
http://localhost:8080

```

You should see the **default NGINX welcome page**.

---

# **2. Modify index.html Inside the Running Container**

### **Step 1: Enter the Container**

```bash
docker exec -it mynginx bash

```

### **Step 2: Navigate to HTML directory**

```bash
cd /usr/share/nginx/html

```

### **Step 3: Edit index.html**

```bash
echo "<h1>Hello from modified container!</h1>" > index.html

```

### **Step 4: Check in browser**

Visit:

```
http://localhost:8080

```

You should now see the **modified page**.

---

# **3. Stop and Restart the Container (Check Persistence)**

### **Step 1: Stop the container**

```bash
docker stop mynginx

```

### **Step 2: Restart it**

```bash
docker start mynginx

```

### **Step 3: Check the website**

Open:

```
http://localhost:8080

```

✔ **Result:**

The modified index.html **PERSISTS** after restart because the container filesystem still exists.

---

# **4. Remove Container and Re-run NGINX (Check Persistence Again)**

### **Step 1: Stop and Remove the Container**

```bash
docker stop mynginx
docker rm mynginx

```

### **Step 2: Run a New NGINX Container**

```bash
docker run --name mynginx -p 8080:80 -d nginx

```

### **Step 3: Check the page**

Visit:

```
http://localhost:8080

```

❌ **Result:**

Your previous modification does **NOT PERSIST**, because the container was deleted.

---

# **5. Achieve Persistence Using Docker Volumes**

Now we test real persistence using volumes.

---

## **Step 1: Create a Volume**

```bash
docker volume create nginx_data

```

## **Step 2: Create a Custom index.html on Host**

```bash
mkdir nginx_site
echo "<h1>Persistent Volume Page</h1>" > nginx_site/index.html

```

## **Step 3: Run NGINX With Volume Mapping**

```bash
docker run --name mynginx \
  -p 8080:80 \
  -v $(pwd)/nginx_site:/usr/share/nginx/html \
  -d nginx

```

### **Check in Browser**

Visit:

```
http://localhost:8080

```

You should see your custom **Persistent Volume Page**.

---

# **6. Test Persistence After Removing Container**

### **Step 1: Stop & Remove the Container**

```bash
docker stop mynginx
docker rm mynginx

```

### **Step 2: Run a New Container With Same Volume Mapping**

```bash
docker run --name mynginx \
  -p 8080:80 \
  -v $(pwd)/nginx_site:/usr/share/nginx/html \
  -d nginx

```

### **Check Again**

Visit:

```
http://localhost:8080

```

✔ **Result:**

The modified index.html **PERSISTS** because the file exists on your host system or the mounted Docker volume.

---

# **Conclusion**

### ✔ Without volumes:

- Data persists only **until container is removed**.
- Restarting does not delete changes, but removing the container does.

### ✔ With volumes:

- Data persists even after the container is removed.
- This is the recommended method for databases, web content, logs, configs, etc.