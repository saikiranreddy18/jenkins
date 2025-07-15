

# Jenkins Setup on AWS EC2 using Amazon Corretto JDK

This guide walks you through setting up Jenkins on an AWS EC2 instance using Amazon Corretto (Java 17).

---

## 🖥️ Prerequisites

- AWS EC2 instance (Ubuntu/Debian)
- A `.pem` key file for SSH access
- Internet connection
- Basic Linux command knowledge

---

## 🚀 Steps to Set Up Jenkins

### 1. 🔐 SSH into your EC2 Instance

```bash
ssh -i "c:/Users/SAI KIRAN/Downloads/mr.pem" ec2-user@ec2-18-209-62-145.compute-1.amazonaws.com
```

---

### 2. 🧰 Install OpenJDK 17

```bash
sudo apt update
sudo apt install -y openjdk-17-jdk
```

---

### 3. 🏗️ Add Amazon Corretto Repository (Optional for updated JDK)

```bash
wget -O- https://apt.corretto.aws/corretto.key | gpg --dearmor | sudo tee /usr/share/keyrings/corretto-archive-keyring.gpg > /dev/null

echo "deb [signed-by=/usr/share/keyrings/corretto-archive-keyring.gpg] https://apt.corretto.aws stable main" | sudo tee /etc/apt/sources.list.d/corretto.list
```

---

### 4. 🔄 Update and Install Amazon Corretto JDK

```bash
sudo apt update
sudo apt install -y java-17-amazon-corretto-jdk
```

---

### 5. 📂 Create Jenkins Directory and Set Permissions

```bash
sudo mkdir -p /opt/jenkins
sudo chown $USER:$USER /opt/jenkins
cd /opt/jenkins
```

---

### 6. 📥 Download Jenkins WAR File

```bash
wget https://get.jenkins.io/war-stable/latest/jenkins.war
```

---

### 7. ▶️ Start Jenkins

```bash
java -jar jenkins.war
```

Jenkins will start on port `8080` by default. You can access it at:

```
http://<your-ec2-public-ip>:8080
```

---

## ✅ Done!

Jenkins is now running on your EC2 instance with Java 17 using Amazon Corretto.
