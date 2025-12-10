# Day 15 – Working With Docker Hub, Image Distribution & Registry Workflow

### **Topics Covered**

- Configuring Docker Hub authentication through CLI and Docker Desktop
- Understanding how container registries manage image layers
- Tagging strategies (`latest`, version tags, semantic versions)
- How Docker handles image metadata, manifests, and digests
- Publishing custom images to Docker Hub for remote access
- Pulling images across different systems and environments

---

## **🔧 Practical Tasks Completed**

### **1. Docker Hub Login**

Authenticated local Docker environment with Docker Hub:

```bash
docker login

```

This stores encrypted credentials in `~/.docker/config.json`.

### **2. Tagging Images for Registry**

Created a properly structured image tag:

```bash
docker tag portfolio laxmanshr2003/portfolio:v1

```

Learned that `repo:tag` format is essential for version control.

### **3. Pushing Images to Docker Hub**

Uploaded the newly tagged image:

```bash
docker push laxmanshr2003/portfolio:v1

```

- Observed how Docker only pushes layers that changed
- Understood layer caching and upload optimization

### **4. Pulling Images**

Tested pulling both official and custom images:

```bash
docker pull nginx
docker pull laxmanshr2003/portfolio:v1

```

### **5. Docker Desktop Usage**

- Verified images in remote registry
- Checked layer history
- Synced Docker Desktop with Docker Hub account
- Monitored push/pull operations visually

---

## **📚 Key Learnings**

- How container registries store and distribute images globally
- Why tagging is critical for versioning and deployment pipelines
- How Docker reuses layers to reduce push/pull time
- Difference between `latest` tag and version-specific tags
- How remote images enable consistent deployment across any machine
- How authentication and credential management work in Docker

---

## **🟢 Summary**

Day 15 provided hands-on experience with Docker Hub as a real-world container registry. I practiced authenticating, tagging, pushing, and pulling images, and gained a deeper understanding of how Docker handles image layers, versioning, and registry distribution. This knowledge is essential for deploying applications across multiple environments and integrating Docker into CI/CD workflows.