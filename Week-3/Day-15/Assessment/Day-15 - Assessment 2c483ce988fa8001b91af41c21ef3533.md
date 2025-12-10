# Day-15 - Assessment

Push portfolio docker image to the docker hub. 

## Step 1: Create an image repository in docker hub

![image.png](images/image.png)

You will find this page after you click  “Create” button

![image.png](images/image%201.png)

## Step 2: Build the image that you want to push to the repository with this command

![image.png](images/image%202.png)

## Step 3: **Tag the Image for Docker Hub**

Used the required naming convention:

`dockerhub-username/repository:tag`

![image.png](images/image%203.png)

## Step 4: Push the docker image to docker hub

![image.png](images/image%204.png)

![image.png](images/image%205.png)

This uploaded all image layers to the remote registry.

---

## **Result**

- The **portfolio image** is successfully published on Docker Hub.
- It can now be pulled on any machine using:
    
    ```bash
    docker pull laxmanshr2003/portfolio:v1
    
    ```