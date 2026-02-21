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

images 
