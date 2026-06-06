# Azure VM Static Website Hosting with Nginx

## Overview

This project demonstrates how to deploy a static website on an Azure Ubuntu Virtual Machine using Nginx.

Through this project, I learned:

* Azure Virtual Machines
* SSH key-based authentication
* Linux basics
* Nginx installation and management
* File transfer using SCP
* Hosting HTML, CSS, and JavaScript files
* Debugging common deployment issues

---

## Architecture

```text
Browser
   ↓
Azure VM (Ubuntu)
   ↓
Nginx
   ↓
Static Website
```

---

## Tech Stack

* Microsoft Azure
* Ubuntu 24.04 LTS
* Nginx
* OpenSSH
* HTML
* CSS
* JavaScript

---

## Steps Performed

### 1. Created an Azure VM

* Ubuntu VM with a public IP
* Enabled:

  * Port 22 (SSH)
  * Port 80 (HTTP)

### 2. Connected to the VM

```bash
ssh -i nginx-key.pem azureuser@<PUBLIC_IP>
```

### 3. Installed Nginx

```bash
sudo apt update
sudo apt install nginx -y
```

Verified:

```bash
systemctl status nginx
```

### 4. Created Website Files

* `index.html`
* `style.css`
* `script.js`

### 5. Uploaded Files Using SCP

```bash
scp -i nginx-key.pem index.html azureuser@<PUBLIC_IP>:/tmp/
scp -i nginx-key.pem style.css azureuser@<PUBLIC_IP>:/tmp/
scp -i nginx-key.pem script.js azureuser@<PUBLIC_IP>:/tmp/
```

### 6. Copied Files to Nginx Directory

```bash
sudo cp /tmp/* /var/www/html/
```

### 7. Accessed the Website

```text
http://<PUBLIC_IP>
```

---

## Issues Faced & Solutions

### SSH Key Permission Error

**Error:**

```text
WARNING: UNPROTECTED PRIVATE KEY FILE!
```

**Solution:**

Modified Windows file permissions using `icacls` and restricted access to the owner.

---

### Permission Denied (publickey)

**Cause:** Incorrect permissions on the `.pem` file.

**Solution:** Fixed ACL permissions and retried SSH.

---

### Old Website Content Still Appeared

**Cause:** Uploaded `index.html` still contained old content.

**Solution:** Updated the file locally and uploaded it again.

---

### favicon.ico 404 Error

**Cause:** Browser requested a favicon that did not exist.

**Impact:** No effect on website functionality.

---

## Key Concepts Learned

* Azure VM provisioning
* SSH authentication
* Linux commands
* Nginx web server
* SCP file transfer
* Port 22 (SSH)
* Port 80 (HTTP)
* Basic troubleshooting

---

## Author

Built as a beginner cloud project to understand Azure, Linux, SSH, and Nginx fundamentals.
