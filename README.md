
# 🚀 Automated Website Deployment with AWS, Jenkins, and GitHub

A fully automated CI/CD pipeline built to deploy static web content to an AWS cloud server instantly upon pushing code changes to GitHub.

---

## 🛠️ Architecture & Tech Stack
* **Cloud Hosting:** AWS EC2 (Ubuntu)
* **Web Server:** Apache HTTP Server
* **CI/CD Automation:** Jenkins (Hosted on EC2)
* **Version Control:** GitHub + Webhooks

---

## 🔄 How It Works
1. Developer makes a code change (e.g., updates `index.html`) locally.
2. Code is pushed to the `main` branch on **GitHub**.
3. GitHub triggers a **Webhook** notifying the **Jenkins** server hosted on AWS.
4. Jenkins automatically clones the repository and deploys the updated files directly to the Apache web root directory (`/var/www/html`), updating the live site instantly.

---

## 🐛 Troubleshooting & Challenges Faced

During the setup of this project, I ran into a couple of real-world roadblocks and fixed them:

### 1. Jenkins Built-In Node Disk Space Warning
* **The Error:** Jenkins threw a red warning banner stating: *"Disk space is below threshold of 1.00 GiB. Only 947.82 MiB out of 952.57 MiB left on /tmp."*
* **The Fix:** Went to **Manage Jenkins** > **Nodes** > **Built-In Node** > **Configure**, and adjusted the **Free Temp Space Threshold** to a lower value (e.g., `500MiB`) to fit the AWS instance's partition limits.

### 2. Sudo Permission Denied in Jenkins Pipeline
* **The Error:** The pipeline failed at the deployment stage because the `jenkins` background user didn't have permission to run `sudo mkdir` without a terminal password prompt (`sudo: a terminal is required to read the password`).
* **The Fix:** Instead of granting risky `sudo` access to Jenkins, I directly assigned proper ownership of the Apache web directory to the `jenkins` user on the EC2 server:
  ```bash
  sudo mkdir -p /var/www/html
  sudo chown -R jenkins:jenkins /var/www/html
  sudo chmod -R 775 /var/www/html
