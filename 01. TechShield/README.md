<div align="center">

# 🛡️ TechShield: VAPT & Digital Forensic Report

**Vulnerability Assessment, Penetration Testing and Forensic Evidence Analysis**

![Target](https://img.shields.io/badge/Target-Metasploitable2-red)
![Attacker](https://img.shields.io/badge/Attacker-Kali%20Linux-purple)
![CVSS](https://img.shields.io/badge/Overall%20CVSS-9.1%20Critical-critical)
![Forensics](https://img.shields.io/badge/Forensics-Autopsy-blue)

</div>

---

## 📖 Overview

This report covers a full security assessment of the **TechShield Corporate Network** lab. A Kali Linux machine was used to attack a Metasploitable2 target, followed by a digital forensic exercise on an evidence image.

It covers three areas:

1. **Vulnerability Assessment:** finding open ports and services
2. **Penetration Testing:** exploiting web and network weaknesses
3. **Digital Forensics:** collecting, verifying and analysing evidence

> ⚠️ **Disclaimer:** All testing was done in an authorized lab and training environment. Do not use these techniques on systems you do not own or have written permission to test.

---

## 🎯 Assessment Details

| Item | Details |
|------|---------|
| **Target** | TechShield Corporate Network (Metasploitable2) |
| **Target IP** | 192.168.171.129 |
| **Attacker Machine** | Kali Linux |
| **Performed by** | Nehal Sarode |
| **Assessment Type** | Network VA, Web App Testing, Password Security, Network Exploitation, Forensic Evidence Collection |
| **Overall Severity** | 🔴 9.1 Critical |

---

## 🧰 Tools Used

| Purpose | Tools |
|---------|-------|
| Host discovery | Netdiscover |
| Port & service scan | Nmap |
| Web app testing | DVWA |
| Password attack | Hydra |
| Remote access | FTP, SSH |
| Evidence creation & hashing | dd, md5sum |
| Forensic analysis | Autopsy |

---

## 🔍 Findings Summary

| # | Vulnerability | Where | CVSS | Severity |
|---|---------------|-------|------|----------|
| 1 | Network & Service Reconnaissance (Information Disclosure) | Multiple open ports | 5.3 | 🟡 Medium |
| 2 | SQL Injection (Data Theft) | DVWA, TCP/80 | 9.8 | 🔴 Critical |
| 3 | Stored Cross-Site Scripting (XSS) | DVWA, TCP/80 | 6.1 | 🟡 Medium |
| 4 | Remote Code Execution via Unrestricted File Upload | DVWA, TCP/80 | 9.8 | 🔴 Critical |
| 5 | Weak / Default Credentials | FTP (21), SSH (22) | 9.8 | 🔴 Critical |

---

## 🧪 What Was Done (Step by Step)

### 1️⃣ Reconnaissance
- Found the target IP using **Netdiscover**
- Scanned open ports and service versions using **Nmap**

### 2️⃣ SQL Injection
- Opened DVWA and set the security level to Low
- Ran a UNION-based SQL injection query
- Dumped usernames and password hashes from the database

### 3️⃣ Stored XSS
- Submitted a script payload in the guestbook
- The script ran in the browser and exposed the visitor's cookie

### 4️⃣ Remote Code Execution
- Created a simple PHP web shell
- Uploaded it through DVWA's upload page, which had no file checks
- Ran a command through the shell and confirmed code execution as `www-data`

### 5️⃣ Weak Credentials
- Brute-forced FTP login with **Hydra**
- Logged into FTP and SSH using the same weak default credentials

### 6️⃣ Digital Forensics
- Created a 50 MB evidence image using `dd`
- Generated an **MD5 hash** of the image
- Loaded the image into **Autopsy** as a new case and host
- Verified the image integrity (original and current hashes matched)
- Found and extracted deleted files
- Sorted files by type to find hidden or renamed files
- Re-checked the hash at the end to confirm the evidence was unchanged

---

## 💥 Impact

| Vulnerability | What an attacker can do |
|---------------|--------------------------|
| Reconnaissance | Learn which hosts, ports and services exist, then pick targets |
| SQL Injection | Read usernames and password hashes from the database |
| Stored XSS | Run scripts in visitors' browsers, steal sessions, hijack accounts |
| File Upload RCE | Run operating-system commands on the server |
| Weak Credentials | Get logged-in access and a remote shell |

---

## 🛠️ Remediation

| Vulnerability | How to fix it |
|---------------|---------------|
| Reconnaissance | Close unused ports, use firewalls, segment the network, deploy IDS/IPS |
| SQL Injection | Use prepared statements, validate input, give the database least privilege |
| Stored XSS | Sanitize input, encode output, use CSP and HttpOnly cookies |
| File Upload RCE | Validate uploads, store files outside the web root, disable script execution |
| Weak Credentials | Remove default accounts, enforce strong passwords, enable account lockout, use SSH keys |

---

## 📚 References

- CWE-200: Information Exposure
- OWASP: SQL Injection
- OWASP: Cross-Site Scripting (XSS)
- OWASP: Unrestricted File Upload
- CWE-521: Weak Password Requirements

---

---

<div align="center">

⭐ **If this helped you learn, give the repo a star!** ⭐

</div>
