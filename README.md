# 🚀 Jenkins on AWS EC2 (Ubuntu) - Setup Guide

This guide walks you through setting up **Jenkins** on an **AWS EC2 instance** running **Ubuntu 20.04/22.04 LTS**.

---

## ✅ Prerequisites

- AWS Account
- EC2 instance with **Ubuntu** (20.04 or 22.04 LTS)
- Security Group with these inbound rules:
  - **SSH**: TCP 22
  - **Jenkins**: TCP 8080
  - *(Optional)*: TCP 80/443 for web access

---

## 🧭 Setup Instructions

### 1. SSH into the EC2 Instance
```bash
ssh -i your-key.pem ubuntu@<your-ec2-public-ip>
```

---

### 2. Update System Packages
```bash
sudo apt update && sudo apt upgrade -y
```

---

### 3. Install Java (Required by Jenkins)
```bash
sudo apt install openjdk-17-jdk -y
```

---

### 4. Add Jenkins Repository and GPG Key
```bash
curl -fsSL https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key | sudo tee /usr/share/keyrings/jenkins-keyring.asc > /dev/null

echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/ | sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
```

---

### 5. Install Jenkins
```bash
sudo apt update
sudo apt install jenkins -y
```

---

### 6. Start and Enable Jenkins
```bash
sudo systemctl start jenkins
sudo systemctl enable jenkins
```

---

### 7. Open Port 8080 in AWS Security Group

- Go to **EC2 > Security Groups > Inbound Rules**
- Add rule:
  - Type: **Custom TCP**
  - Port Range: **8080**
  - Source: **0.0.0.0/0** (or your IP for better security)

---

### 8. Access Jenkins in Your Browser

```
http://<your-ec2-public-ip>:8080
```

---

### 9. Get Initial Admin Password
```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```
- Paste this password in the Jenkins setup page.

---

### 10. Install Plugins and Create Admin User

- Choose **"Install suggested plugins"**
- Create your Jenkins admin user

---

## 🔒 Optional: Nginx Reverse Proxy + SSL (Let’s Encrypt)

If you want a custom domain (e.g. `jenkins.yourdomain.com`) with HTTPS:

- Install Nginx
- Configure domain pointing
- Add Let’s Encrypt SSL

> Let me know if you want help setting that up!

---

## 🛠️ Jenkins Is Ready!

You now have a working Jenkins server on your Ubuntu EC2 instance.

Happy Automating! 🚀
