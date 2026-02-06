
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

## 📚 API Scope & Assumptions
- REST-based API
- Supports common HTTP methods: `GET`, `POST`, `PUT`, `DELETE`
- Uses token-based authentication (e.g., JWT / Bearer Token)
- Returns standard HTTP response codes
- Testing performed in a **non-production environment**

---

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
