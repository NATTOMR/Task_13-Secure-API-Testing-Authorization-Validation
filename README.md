
# Task 13: Secure API Testing & Authorization Validation

## 📌 Project Overview
This project focuses on **testing REST API security controls**, with an emphasis on **authentication, authorization, input validation, and rate limiting**. The goal is to identify common API misconfigurations and vulnerabilities using industry-standard tools and methodologies.

All testing is performed from a **black-box perspective**, simulating how an attacker or security tester would interact with exposed API endpoints.

---

## 🎯 Objectives
- Understand how REST APIs handle authentication and authorization
- Validate access control mechanisms
- Identify broken authorization scenarios
- Test API input validation and error handling
- Detect missing or weak rate limiting protections
- Map findings to **OWASP API Security Top 10**

---

## 🛠️ Tools Used
- **Postman** (Primary)
- **cURL** (Alternative)
- **Insomnia** (Alternative)

---
# Install Postman on Kali Linux

This guide provides step‑by‑step instructions to install **Postman** on Kali Linux.

---

## 📌 Method 1 — Install Postman via Snap (Recommended)

### Step 1: Update System Packages

```bash
sudo apt update && sudo apt upgrade -y
```

### Step 2: Install Snapd

```bash
sudo apt install snapd -y
```

### Step 3: Enable & Start Snap Service

```bash
sudo systemctl enable --now snapd
```

### Step 4: Install Postman

```bash
sudo snap install postman
```

### Step 5: Launch Postman

```bash
postman
```

---

## 📌 Method 2 — Install Postman Manually (Official Tar Package)

### Step 1: Download Postman

```bash
wget https://dl.pstmn.io/download/latest/linux64 -O postman.tar.gz
```

### Step 2: Extract the Archive

```bash
sudo tar -xzf postman.tar.gz -C /opt
```

### Step 3: Create Symbolic Link

```bash
sudo ln -s /opt/Postman/Postman /usr/bin/postman
```

### Step 4: Launch Postman

```bash
postman
```

---

## 📌 (Optional) Create Desktop Entry

Create a desktop shortcut so Postman appears in the application menu.

```bash
nano ~/.local/share/applications/postman.desktop
```

Paste the following:

```ini
[Desktop Entry]
Name=Postman
Exec=/opt/Postman/Postman
Icon=/opt/Postman/app/resources/app/assets/icon.png
Type=Application
Categories=Development;
```

Save and exit:

* Press **CTRL + O** → Enter
* Press **CTRL + X**

Refresh applications:

```bash
update-desktop-database ~/.local/share/applications
```

---

## ✅ Verify Installation

```bash
postman --version
```

If Postman opens successfully, the installation is complete.
![image](https://github.com/NATTOMR/Task_13-Secure-API-Testing-Authorization-Validation/blob/main/postman%20install.png)
![image](https://github.com/NATTOMR/Task_13-Secure-API-Testing-Authorization-Validation/blob/main/postman%20dashboard.png)
---

## 🧹 Uninstall Postman

### If installed via Snap

```bash
sudo snap remove postman
```

### If installed manually

```bash
sudo rm -rf /opt/Postman
sudo rm /usr/bin/postman
```

---


## 📚 API Scope & Assumptions
- REST-based API
- Supports common HTTP methods: `GET`, `POST`, `PUT`, `DELETE`
- Uses token-based authentication (e.g., JWT / Bearer Token)
- Returns standard HTTP response codes
- Testing performed in a **non-production environment**

---

## 📚 REST-based API
REST API stands for Representational State Transfer API. It is a type of API (Application Programming Interface) that allows communication between different systems over the internet. REST APIs work by sending requests and receiving responses, typically in JSON format, between the client and server.

![image](https://github.com/NATTOMR/Task_13-Secure-API-Testing-Authorization-Validation/blob/main/Rest%20APL.png)
- A request is sent from the client to the server via a web URL, using one of the HTTP methods.
- The server then responds with the requested resource, which could be HTML, XML, Image, or JSON, with JSON being the most commonly used format for modern web services.
- These methods map to CRUD operations (Create, Read, Update, Delete) for managing resources on the web.

## 1. GET Method
The HTTP GET method is used to read (or retrieve) a representation of a resource. In the safe path, GET returns a representation in XML or JSON and an HTTP response code of 200 (OK). In an error case, it most often returns a 404 (NOT FOUND) or 400 (BAD REQUEST).
```GET /users/123
```
This request fetches data for the user with ID 123

## 2. POST Method
The POST method is commonly used to create new resources. It is often used to create subordinate resources related to a parent resource. Upon successful creation, the server returns HTTP status 201 (Created) along with a Location header pointing to the newly created resource.

`` POST /users
{ 
  "name": "Anjali", 
  "email": "gfg@example.com"
} ```

This request creates a new user with the given data.

 NOTE:  POST is neither safe nor idempotent. 

## 3. PUT Method
PUT is an HTTP method used to update or create a resource on the server. When using PUT, the entire resource is sent in the request body, and it replaces the current resource at the specified URL. If the resource doesn’t exist, it can create a new one.

```PUT /users/123
{ 
  "name": "Anjali", 
  "email": "gfg@example.com"
}
```
This request updates the user with ID 123 or creates a new user if one doesn't exist.

## 5. DELETE Method
It is used to delete a resource identified by a URI. On successful deletion, return HTTP status 200 (OK) along with a response body.

```DELETE /users/123
```
This request deletes the user with ID 123.

## 🔍 Testing Methodology

### 1. API Endpoint Configuration
- Imported or manually configured API endpoints in Postman
- Set request headers (`Authorization`, `Content-Type`)
- Constructed request bodies based on API documentation

---

### 2. Authentication Testing
**Tests Performed**
- Valid credentials → Confirm authorized access
- Invalid credentials → Expect `401 Unauthorized`
- Expired token → Expect authentication failure
- Missing authentication header → Verify access denial

**Expected Behavior**
- API should strictly require authentication
- No endpoint should allow unauthenticated access

---

### 3. Authorization Testing (Broken Object Level Authorization - BOLA)
**Tests Performed**
- Modified resource IDs in requests
- Accessed objects belonging to other users
- Tested role-based access (user vs admin endpoints)

**Example**
```http
GET /api/users/123
GET /api/users/124   ← unauthorized user ID
```

**Author:**   NATTO MUNI CHAKMA
**OS:** Kali Linux
**Tool:** Postman API Client
-------------


