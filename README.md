<p align="center">
  <img src="API banner.png" alt="API Security Testing Lab Banner">
</p>


<p align="center">
  <img src="https://img.shields.io/badge/API%20Security-OWASP%20Top%2010-red?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/Tool-Postman-orange?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/OS-Kali%20Linux-blue?style=for-the-badge"/>
</p>

<h1 align="center">🔐 Secure API Testing & Authorization Validation</h1>

<p align="center">
  A hands-on cybersecurity project focused on identifying authentication, authorization,
  input validation, and rate limiting issues in REST APIs using OWASP API Security Top 10.
</p>

---

# Secure API Testing & Authorization Validation

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
```
GET natto
```
This request fetches data for the user with ID 123

## ✅ STEP 1: Add a FREE GET URL (Do This First)

In the middle of your screen you see:

```
GET   Enter URL or paste text   [Send]
```

- 👉 Click inside “Enter URL or paste text”

Paste this free API URL:

```
 https://httpbin.org/get
```
## ✅ STEP 2: Send the Request

- Click the blue Send button.

- What should happen:

- At the bottom (Response section), you should see:

- Status: 200 OK

- Response body (JSON)

  ![image](https://github.com/NATTOMR/Task_13-Secure-API-Testing-Authorization-Validation/blob/main/postman%20dash-2.png)
-  Example:
   
  ```
{
    "args": {
        "": "tester",
        "role": "natto"
    },
    "headers": {
        "Accept": "*/*",
        "Accept-Encoding": "gzip, deflate, br",
        "Cache-Control": "no-cache",
        "Host": "httpbin.org",
        "Postman-Token": "5987e34c-da8b-4ea3-870d-15dbee5054f5",
        "User-Agent": "PostmanRuntime/7.51.1",
        "X-Amzn-Trace-Id": "Root=1-69872bd6-0edf1768792dcbdc16dbf9d3"
    },
    "origin": "106.200.28.147",
    "url": "https://httpbin.org/get?role=natto&=tester"
}
```
![image](https://github.com/NATTOMR/Task_13-Secure-API-Testing-Authorization-Validation/blob/main/postman%20dash-3.png)

### Note: GET returns a representation in XML or JSON and an HTTP response code of 200 (OK)

## 2. POST Method
The POST method is commonly used to create new resources. It is often used to create subordinate resources related to a parent resource. Upon successful creation, the server returns HTTP status 201 (Created) along with a Location header pointing to the newly created resource.
POST user natto-2
```
{
    "args": {
        "tester": "natto"
    },
    "data": "{\n  \"username\": \"natto\",\n  \"role\": \"tester\"\n}\n",
    "files": {},
    "form": {},
    "headers": {
        "Accept": "*/*",
        "Accept-Encoding": "gzip, deflate, br",
        "Cache-Control": "no-cache",
        "Content-Length": "46",
        "Content-Type": "application/json",
        "Host": "httpbin.org",
        "Postman-Token": "69c67ce9-b4b6-4bec-aa78-ff4b5cdbfee6",
        "User-Agent": "PostmanRuntime/7.51.1",
        "X-Amzn-Trace-Id": "Root=1-698732eb-14a9ea320b8076dd60603ccc"
    },
    "json": {
        "role": "tester",
        "username": "natto"
    },
    "origin": "106.200.28.147",
    "url": "https://httpbin.org/post?tester=natto"
}
```
This request creates a new user with the given data.

![image](https://github.com/NATTOMR/Task_13-Secure-API-Testing-Authorization-Validation/blob/main/post.png)

 NOTE:  POST is neither safe nor idempotent. 

## 3. PUT Method
PUT is an HTTP method used to update or create a resource on the server. When using PUT, the entire resource is sent in the request body, and it replaces the current resource at the specified URL. If the resource doesn’t exist, it can create a new one.

`PUT user natto-1`
```
{
    "args": {
        "tester": "natto"
    },
    "data": "",
    "files": {},
    "form": {},
    "headers": {
        "Accept": "*/*",
        "Accept-Encoding": "gzip, deflate, br",
        "Cache-Control": "no-cache",
        "Content-Length": "0",
        "Host": "httpbin.org",
        "Postman-Token": "b11b9d88-5878-4444-a3bf-c67acd41b30b",
        "User-Agent": "PostmanRuntime/7.51.1",
        "X-Amzn-Trace-Id": "Root=1-6987341a-06e8de1f711f0cc65fffc5b4"
    },
    "json": null,
    "origin": "106.200.28.147",
    "url": "https://httpbin.org/put?tester=natto"
}
```
![image](https://github.com/NATTOMR/Task_13-Secure-API-Testing-Authorization-Validation/blob/main/put.png)
Note:

## 4. PATCH Method
PATCH is an HTTP method used to partially update a resource on the server. Unlike PUT, PATCH only requires the fields that need to be updated to be sent in the request body. It modifies specific parts of the resource rather than replacing the entire resource.

`PATCH user natto-3`
```
{
    "args": {
        "tester": "natto"
    },
    "data": "",
    "files": {},
    "form": {},
    "headers": {
        "Accept": "*/*",
        "Accept-Encoding": "gzip, deflate, br",
        "Cache-Control": "no-cache",
        "Content-Length": "0",
        "Host": "httpbin.org",
        "Postman-Token": "98624f42-2a42-4889-9774-685b7845a5d9",
        "User-Agent": "PostmanRuntime/7.51.1",
        "X-Amzn-Trace-Id": "Root=1-698734fb-1bb793e709265878318b26f2"
    },
    "json": null,
    "origin": "106.200.28.147",
    "url": "https://httpbin.org/patch?tester=natto"
}
```
![image](https://github.com/NATTOMR/Task_13-Secure-API-Testing-Authorization-Validation/blob/main/patch.png)

## 5. DELETE Method
It is used to delete a resource identified by a URI. On successful deletion, return HTTP status 200 (OK) along with a response body.

`PUT user natto-1`
```
{
    "args": {
        "tester": [
            "natto",
            "natto"
        ]
    },
    "data": "",
    "files": {},
    "form": {},
    "headers": {
        "Accept": "*/*",
        "Accept-Encoding": "gzip, deflate, br",
        "Cache-Control": "no-cache",
        "Host": "httpbin.org",
        "Postman-Token": "7f8ffbe5-a3a3-4bf1-bfb8-728ee1af9a0a",
        "User-Agent": "PostmanRuntime/7.51.1",
        "X-Amzn-Trace-Id": "Root=1-6987354a-6246650c57eaa37773c9493b"
    },
    "json": null,
    "origin": "106.200.28.147",
    "url": "https://httpbin.org/delete?tester=natto&tester=natto"
}
```
![image](https://github.com/NATTOMR/Task_13-Secure-API-Testing-Authorization-Validation/blob/main/delete.png)

## 🔍 Testing Methodology

### 1. API Endpoint Configuration
- Imported or manually configured API endpoints in Postman
- Set request headers (`Authorization`, `Content-Type`)
- Constructed request bodies based on API documentation

---

## 🔐 Authentication Testing

### Endpoint
- URL: `https://httpbin.org/bearer`
- Auth tab → Bearer Token
- Token: testtoken123
- Response: 200 OK
  ![image](https://github.com/NATTOMR/Task_13-Secure-API-Testing-Authorization-Validation/blob/main/authentication.png)

  Note: 🎉 Authentication test PASSED

### Test Case 1: Valid Authentication
- Authorization: Bearer Token
- Result: 200 OK
- Observation: Authenticated access allowed

### Test Case 2: Missing Authentication
- Go to Auth tab
- Change Auth Type → No Auth
- Authorization header removed
- Result: 401 Unauthorized
- Observation: Unauthenticated access denied
  ![image](https://github.com/NATTOMR/Task_13-Secure-API-Testing-Authorization-Validation/blob/main/authentication-1.png)

  Note: ✔ This proves unauthenticated access is blocked

**Expected Behavior**
- API should strictly require authentication
- No endpoint should allow unauthenticated access

## 🔐 Authentication Header Removal Test

### Test Description
The authentication header was removed and the request was resent to verify whether the API improperly allows unauthenticated access.
- Auth Type: No Auth
- URL: /bearer
- Response: 401 Unauthorized
  ![image](https://github.com/NATTOMR/Task_13-Secure-API-Testing-Authorization-Validation/blob/main/without%20token.png)
### Result
- Authorization: Removed
- HTTP Status: 401 Unauthorized
- Observation: Access denied without authentication


---

## 🔓 Authorization Testing (Broken Object Level Authorization – BOLA)

### Endpoint
https://jsonplaceholder.typicode.com/users/{id}

### Test Description
Object identifiers in the API endpoint were modified to test whether unauthorized access to other users’ data was possible.

### Test Cases
- GET /users/1 → 200 OK
- ![image](https://github.com/NATTOMR/Task_13-Secure-API-Testing-Authorization-Validation/blob/main/BOLA%20-1.png)
- GET /users/2 → 200 OK
- ![image](https://github.com/NATTOMR/Task_13-Secure-API-Testing-Authorization-Validation/blob/main/BOLA%20-2.png)

### Observation
The API returned data for different user IDs when the object identifier was modified.

### Security Analysis
In a real-world authenticated environment, this behavior could lead to Broken Object Level Authorization if proper access controls are not enforced.



### Expected Secure Behavior
The API should validate ownership and return `403 Forbidden` for unauthorized object access.

## 🧪 Input Validation Testing

### Endpoint
`https://httpbin.org/post`

### Test Description
Malformed and unexpected input values were sent to evaluate server-side input validation controls.

### Test Cases
**Valid Input**
```json
{
  "username": "natto",
  "role": "tester"
}
```
![image](https://github.com/NATTOMR/Task_13-Secure-API-Testing-Authorization-Validation/blob/main/valid%20input.png)

Note: The initial POST request returned `"json": null`, indicating that no request body was sent.
After configuring the request body using raw JSON format, the API correctly received and processed the input.
Malformed input values were also accepted, highlighting the importance of strict server-side input validation in real-world APIs.

## 🚦 Rate Limiting Testing

### Endpoint
https://httpbin.org/get
![image](https://github.com/NATTOMR/Task_13-Secure-API-Testing-Authorization-Validation/blob/main/rate%20limiting.png)
### Test Description
Multiple rapid requests were sent to the API endpoint to evaluate rate limiting and abuse prevention mechanisms.

### Observation
The API responded with `200 OK` for all repeated requests, indicating that no rate limiting was enforced.

### Security Analysis
In a real-world environment, the absence of rate limiting could allow brute-force attacks and denial-of-service conditions.

### Expected Secure Behavior
The API should restrict excessive requests and return `429 Too Many Requests`.

OWASP Mapping: API4 – Lack of Resources & Rate Limiting


## ✅ Final Answer (One Line)

You check 429 Too Many Requests by sending many requests quickly; if it never appears, rate limiting is not enforced and should be documented as a risk.

## ⚠️ Disclaimer

This project is for educational and ethical testing purposes only. All testing was conducted using public test APIs in non-production environments.

## 📎 References & Learning Resources

This project was completed using publicly available documentation, public test APIs, and industry-recognized security standards related to REST API security testing.

---

### 🔐 OWASP API Security
- **OWASP API Security Top 10**  
  https://owasp.org/API-Security/

- **OWASP API Security Top 10 – GitHub Repository**  
  https://github.com/OWASP/API-Security

---

### 🌐 Public Test APIs Used
- **httpbin** – HTTP request & response testing service  
  https://httpbin.org/

- **JSONPlaceholder** – Fake REST API for testing and prototyping  
  https://jsonplaceholder.typicode.com/

---

### 🧪 API Testing Tools
- **Postman Official Documentation**  
  https://learning.postman.com/

- **Postman API Client Downloads**  
  https://www.postman.com/downloads/

- **cURL Manual**  
  https://curl.se/docs/manual.html

---

### 📚 REST API Fundamentals
- **REST API Concepts – Mozilla Developer Network (MDN)**  
  https://developer.mozilla.org/en-US/docs/Glossary/REST

- **HTTP Methods Overview – MDN**  
  https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods

- **HTTP Status Codes – MDN**  
  https://developer.mozilla.org/en-US/docs/Web/HTTP/Status

---

### 🚦 Rate Limiting & API Security Concepts
- **API Rate Limiting Explained (MDN)**  
  https://developer.mozilla.org/en-US/docs/Web/HTTP/Headers/Retry-After

- **OWASP – API Abuse & Rate Limiting Risks**  
  https://owasp.org/www-project-api-security/

---

### 🛡️ Authorization & Access Control
- **Broken Object Level Authorization (BOLA)**  
  https://owasp.org/API-Security/editions/2023/en/0xa1-broken-object-level-authorization/

- **Broken Authentication**  
  https://owasp.org/API-Security/editions/2023/en/0xa2-broken-authentication/

---


## 👨‍💻 Author

**NATTO MUNI CHAKMA**  
Cybersecurity Enthusiast | API Security | Kali Linux | OWASP

---



