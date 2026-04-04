# DVWA Deployment on EC2.

## 🏗️ Architecture

* EC2 (Ubuntu 22.04)
* Apache Web Server
* MySQL Database
* PHP Application (DVWA)

---

## ⚙️ Installation Steps

### Update System

```bash
sudo apt update && sudo apt upgrade -y
```

### Install LAMP Stack

```bash
sudo apt install apache2 mysql-server php php-mysqli php-gd libapache2-mod-php git -y
```

### Start Apache

```bash
sudo systemctl start apache2
sudo systemctl enable apache2
```

---

## 🗄️ Database Setup

```sql
CREATE DATABASE dvwa;
CREATE USER 'dvwa'@'localhost' IDENTIFIED BY 'password';
GRANT ALL PRIVILEGES ON dvwa.* TO 'dvwa'@'localhost';
FLUSH PRIVILEGES;
```

---

## 📦 DVWA Setup

```bash
cd /var/www/html
sudo git clone https://github.com/digininja/DVWA.git
```

---

## 🔐 Configuration Changes

Updated `config.inc.php`:

```php
$_DVWA[ 'db_user' ] = 'dvwa';
$_DVWA[ 'db_password' ] = 'password';
```

---

## ⚠️ Security Observations

* Weak credentials used intentionally
* Application vulnerable by design
* Public exposure will be controlled

---

## 🧠 Key Learnings

* LAMP stack setup
* Database-user privilege separation
* Web app deployment in cloud

---

## 🚨 Attack Simulation Results

### 🔍 Recon

* Nmap scan identified open ports: 22 (SSH), 80 (HTTP)

### 🧪 Scans

* Nikto web vulnerability scan executed

### 💣 Attacks Performed

* SQL Injection
* Cross-Site Scripting (XSS)
* Brute Force login attempts

### 🧠 Observation

Application responds to malicious inputs, confirming vulnerable behavior

### 🎯 Outcome

Successfully generated attack traffic for SOC monitoring


## ✅ Result

DVWA successfully deployed and accessible via:
http://<EC2-PUBLIC-IP>/DVWA
