# 🔗 Jenkins-GitHub CI Integration (Freestyle Job with Webhook)

This repository documents the setup of a **Continuous Integration (CI) pipeline** using **Jenkins** and **GitHub**.  
It demonstrates how Jenkins automatically triggers a build whenever new code is pushed to this GitHub repository via a **webhook**.

---

## 🧠 Overview

This setup connects:
- **GitHub (Source Control)** → Hosts the code repository.
- **Jenkins (CI Tool)** → Fetches code, runs automated builds/tests, and provides real-time build feedback.

By the end, each push to GitHub will trigger Jenkins automatically, achieving **Continuous Integration**.

---

## 🧩 Prerequisites

Ensure you already have:

- Jenkins running on **AWS EC2 (Ubuntu 22.04)** or any Linux host  
- Jenkins is accessible on port **8080**
- **Git** installed on the Jenkins server  
- Your GitHub repository (public or private) ready  
- Basic Jenkins plugins installed:
  - 🧩 **Git Plugin**
  - 🧩 **GitHub Integration Plugin**
  - 🧩 **GitHub API Plugin**

---

## ⚙️ Step-by-Step Setup

### 🪜 Step 1: Create a GitHub Repository
1. Go to [GitHub → New Repository](https://github.com/new).
2. Name it: **`Jenkins-GitHub-Integration-WebHook`**
3. Initialize with:
   - ✅ A README file
   - ✅ Public visibility (for simplicity)

📸 *Screenshot Placeholder:* `create_repo.png`

---

### 🧑‍💻 Step 2: Create a Jenkins Freestyle Job
1. Open Jenkins → **New Item**
2. Name it: **`demo-build`**
3. Select: **Freestyle Project**
4. Click **OK**

📸 *Screenshot Placeholder:* `jenkins_new_item.png`

---

### 🧠 Step 3: Configure Source Code Management (Git)
1. In your Jenkins job → Select **Git** under “Source Code Management”
2. Enter your repository URL:
https://github.com/<your-username>/jenkins-demo.git
3. For Branches to build:
*/main
4. Save the configuration.

📸 *Screenshot Placeholder:* `jenkins_git_config.png`

---

### 🧱 Step 4: Add Build Step
1. Scroll to the **Build** section.
2. Click **Add build step → Execute shell**
3. Enter:
```bash
echo "=============================="
echo "Build started on: $(date)"
echo "Repository contents:"
ls -la
echo "Running sample script if exists..."
bash build.sh || echo "No build.sh found!"
echo "Build finished successfully!"
echo "=============================="
```
Save the job.

📸 Screenshot Placeholder: jenkins_build_step.png


### 🔔 Step 5: Set Up GitHub Webhook
Go to your GitHub repo → Settings → Webhooks → Add webhook

In the Payload URL, enter:
http://<your-ec2-public-ip>:8080/github-webhook/
Select:
Content type: application/json
Trigger: “Just the push event”
Click Add Webhook

📸 Screenshot Placeholder: github_webhook.png

### 🧪 Step 6: Verify Integration
Push a small change to your repo (e.g., edit README.md).
Check Jenkins:
The job should trigger automatically.
Console output should show the new build running successfully.

📸 Screenshot Placeholder: jenkins_build_success.png

✅ Expected Output (Console Log Example)
Started by GitHub push by Sarthak Srivastava
Building in workspace /var/lib/jenkins/workspace/demo-build
 > git fetch --tags --force --progress -- https://github.com/SarthakSrivastava3005/jenkins-demo.git +refs/heads/*:refs/remotes/origin/*
Checking out Revision <commit-id> (refs/remotes/origin/main)
+ echo Build started on: Wed Nov 5 10:52:39 UTC 2025
+ echo Repository contents:
+ ls -la
+ bash build.sh
Hello from Jenkins build job!
+ echo Build finished successfully!
Finished: SUCCESS

## 🧾 References
Jenkins Documentation

GitHub Webhooks Guide

AWS EC2 User Guide

## 👨‍💻 Author
Sarthak Srivastava
Java Backend & Cloud Enthusiast | Exploring DevOps & AWS Cloud
📧 srivastava.sarthak.2000@gmail.com
🔗 LinkedIn

⭐ If this helped you set up Jenkins–GitHub CI, please give it a star on GitHub!
