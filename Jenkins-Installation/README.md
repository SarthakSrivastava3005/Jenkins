# 🚀 Jenkins Installation & Setup on AWS EC2 (Ubuntu)

This repository documents the setup and configuration of **Jenkins**, an open-source automation server, on an **AWS EC2 instance** running **Ubuntu 22.04 LTS**.  
It demonstrates key steps of a typical **DevOps CI/CD environment setup** using AWS and Linux.

---

## 🧠 Project Overview

The goal of this task is to deploy and configure **Jenkins**, an essential CI/CD tool on a cloud-based virtual machine (AWS EC2).  
This setup allows developers to automate build, test, and deployment pipelines.

---

## 🧩 Prerequisites

Before starting, ensure you have:

- An active [AWS account](https://aws.amazon.com/)
- A running **EC2 instance (Ubuntu 22.04 or later)**  
- A valid **key pair (.pem)** file for SSH access  
- Port **22 (SSH)** and **8080 (Jenkins)** open in your EC2 **Security Group**

---

## ⚙️ Steps to Install Jenkins

```bash
1. SSH into the EC2 Instance
ssh -i /path/to/your-key.pem ubuntu@<your-ec2-public-ip>

Tip: If SSH fails, check your Security Group inbound rules.
Port 22 must be open for your public IP (or 0.0.0.0/0 for testing only).

2. Update System Packages
sudo apt update && sudo apt upgrade -y

3. Install Java (Jenkins Dependency)
sudo apt install openjdk-11-jdk -y
java -version

4. Add Jenkins Repository Key and Source List
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc \
  https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key

echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian-stable binary/" | \
  sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null

5. Install Jenkins
sudo apt update
sudo apt install jenkins -y

6. Start and Enable Jenkins Service
sudo systemctl start jenkins
sudo systemctl enable jenkins
sudo systemctl status jenkins
Ensure Jenkins is active and running successfully.
```
### 7. Access Jenkins inside Browser
Open your browser and visit:

http://<your-ec2-public-ip>:8080

### 8. Unlock Jenkins
Get the initial admin password:
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
Copy the password, paste it into the browser field, and continue setup.

### 9. Install Suggested Plugins and Create Admin User
Click “Install suggested plugins”
Create your Jenkins admin credentials
Configure instance URL as your EC2 public IP (port 8080)

---

## Verification
After installation, verify Jenkins dashboard is accessible:

✅ Jenkins service is running
✅ Web UI loads at port 8080
✅ Plugins and credentials configured successfully

---

## 🧾 References
Jenkins Official Documentation

AWS EC2 User Guide

OpenJDK Installation

---

## 👨‍💻 Author
Sarthak Srivastava
Java Backend & Cloud Enthusiast | Exploring DevOps & AWS Cloud
📧 srivastava.sarthak.2000@gmail.com
🔗 https://www.linkedin.com/in/sarthak-srivastava-developer/

---

## Next Steps
Integrate Jenkins with GitHub for source code automation

Configure build pipelines using Maven/Gradle

Deploy builds to AWS S3 / EC2 / EKS for CI/CD

Automate with Infrastructure as Code (IaC) using Terraform or CloudFormation

---

⭐ If you found this useful, give this repo a star!
