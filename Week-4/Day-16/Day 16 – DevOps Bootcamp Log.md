# Day 16 – DevOps Bootcamp Log

Today’s session was mainly focused on understanding **multi-stage Docker builds**, versioning concepts, dependency management, and the difference between `npm install` and `npm ci`. These topics helped me understand how production-grade applications are built and optimized.

---

## **1. Multi-Stage Dockerfile (Multibuild)**

Today I learned how multi-stage builds help create efficient Docker images.

Instead of creating one heavy image, we split the build into multiple stages:

- **Builder stage:** compiles, installs dependencies
- **Final stage:** only keeps the required output (ex: `dist/` folder)

This reduces image size and improves security.

Example I practiced:

```docker
# Stage 1 – Builder
FROM node:18 AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build

# Stage 2 – Production
FROM nginx:alpine
COPY --from=builder /app/dist /usr/share/nginx/html

```

This helped me understand how companies optimize images for deployment.

---

## **2. Versioning & Its Types**

We discussed versioning systems and how they are used in projects.

### **Semantic Versioning (SemVer)**

This is the most common format:

`MAJOR.MINOR.PATCH`

Examples:

- `1.0.0` – first stable release
- `1.1.0` – backward-compatible feature added
- `1.1.5` – bug fix

I also learned the difference between:

### **package.json**

- Stores dependencies **with flexible version ranges**
- Example: `"express": "^4.18.0"`

### **package-lock.json**

- Stores **exact versions** installed in the system
- Ensures every developer/server installs **the same versions**

This is critical for consistency, especially in production.

---

## **3. Difference Between `npm ci` and `npm install`**

Today I finally understood when to use which command:

### **npm install**

- Installs dependencies from `package.json`
- Updates `package-lock.json` if necessary
- Good for development

### **npm ci**

- Installs dependencies **exactly** as per `package-lock.json`
- Faster and predictable
- Used in: CI/CD pipelines, production images, Docker builds

Example from Dockerfile:

```docker
RUN npm ci
```

This ensures the build is reproducible every time.

---

## **4. Why Dependencies Are Important**

Dependencies are the external libraries that our application needs to run.

Today I understood their importance clearly:

- Avoid reinventing code
- Faster development
- Stable and tested features
- Industry-grade reliability
- Maintains consistency across environments
- Prevents unexpected bugs when versions change
- Ensures the app builds the same way everywhere (local, CI, production)

I also realized how dependency issues can break builds, create security problems, or cause version conflicts—so managing them properly is a key skill in DevOps.

---

## **Summary**

Today I got a much better understanding of:

- How multi-stage Docker builds optimize production images
- How versioning works and why SemVer matters
- The role of `package.json` vs `package-lock.json`
- The exact use case of `npm install` vs `npm ci`
- Why dependency management is essential in DevOps pipelines