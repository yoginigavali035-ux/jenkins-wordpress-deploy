# 🚀 WordPress Deployment using Jenkins (Without Docker)

## 📌 Project Overview

This project demonstrates how to deploy **WordPress** on an Ubuntu EC2 instance using **Jenkins Pipeline**.

The pipeline automatically:
- Connects to EC2 via SSH
- Installs Apache, PHP, MySQL
- Creates WordPress database
- Downloads and configures WordPress
- Sets file permissions
- Restarts Apache

---

## 🛠 Technologies Used

- Jenkins
- Apache2
- MySQL
- PHP
- Ubuntu EC2
- GitHub

---

## 🏗 Architecture

Developer → GitHub → Jenkins → EC2 Server → Apache → WordPress

---

## ⚙ Prerequisites

- Ubuntu EC2 Instance
- Jenkins Installed
- SSH Key added in Jenkins Credentials
- Port 80 open in Security Group

---

## 🔐 Jenkins Credentials

Add your SSH private key in:

Manage Jenkins → Credentials → Global → Add Credentials

Type: SSH Username with Private Key

---

## 📂 Project Structure

jenkins-wordpress-deploy/
│
├── Jenkinsfile
└── README.md



## 🧠 What I Learned

- Jenkins Pipeline scripting
- SSH Agent Plugin usage
- Automating WordPress installation
- MySQL database automation
- CI/CD concepts
- Linux server configuration

---

## images 

![img alt](https://github.com/yoginigavali035-ux/jenkins-wordpress-deploy/blob/main/images/server.png)

![img alt](https://github.com/yoginigavali035-ux/jenkins-wordpress-deploy/blob/main/images/credintial.png)

![img alt](https://github.com/yoginigavali035-ux/jenkins-wordpress-deploy/blob/main/images/webhook.png)

![img alt](https://github.com/yoginigavali035-ux/jenkins-wordpress-deploy/blob/main/images/jenkins%20file.png)

![img alt](https://github.com/yoginigavali035-ux/jenkins-wordpress-deploy/blob/main/images/create%20job.png)

![img alt](https://github.com/yoginigavali035-ux/jenkins-wordpress-deploy/blob/main/images/connect%20to%20github.png)

---
## 🛠 Troubleshooting Experience

During the project implementation, I faced and resolved the following issues:

### 🔴 1️⃣ Jenkins Could Not Connect to GitHub Repository

**Issue:**  
Jenkins failed to fetch the repository during pipeline execution.

**Root Cause:**  
Incorrect repository path and branch configuration in Jenkins pipeline settings.

**Solution:**  
- Verified the correct GitHub repository URL  
- Checked the branch name (`main`)  
- Corrected the pipeline script path in Jenkins configuration  
- Rebuilt the pipeline successfully  

**Learning:**  
Always verify SCM configuration, branch name, and repository access before triggering builds

![img alt](https://github.com/yoginigavali035-ux/jenkins-wordpress-deploy/blob/main/images/troubleshooting.png)

### 🔴 2️⃣ WordPress Database Connection Failed

**Issue:**  
WordPress showed "Error establishing a database connection".

**Root Cause:**  
Incorrect database username and password configured in `wp-config.php`.

**Solution:**  
- Verified MySQL database and user credentials  
- Corrected database name, username, and password  
- Updated `wp-config.php` configuration  
- Restarted Apache service  

**Learning:**  
Database credentials must exactly match the MySQL configuration. Small mistakes in username or password cause application failure.

![img alt](https://github.com/yoginigavali035-ux/jenkins-wordpress-deploy/blob/main/images/database%20connectin%20fail.png)

---

## succesfully deploy

![img alt](https://github.com/yoginigavali035-ux/jenkins-wordpress-deploy/blob/main/images/build%20success.png)

![img alt](https://github.com/yoginigavali035-ux/jenkins-wordpress-deploy/blob/main/images/successfully%20%20connected%20wordpress.png)

![img alt](https://github.com/yoginigavali035-ux/jenkins-wordpress-deploy/blob/main/images/wordpress.png)

![img alt](https://github.com/yoginigavali035-ux/jenkins-wordpress-deploy/blob/main/images/final%20output.png)

---
