
# 🚀 Deployment Guide for Java Web Application on AWS EC2

This guide explains how to set up and deploy your Java web application using **Git**, **Jenkins**, **Ansible**, and **Apache Tomcat** on an AWS EC2 instance.

---

## 📁 Repository Structure

| File/Folder         | Purpose                                                                 |
|---------------------|-------------------------------------------------------------------------|
| `src/main/webapp`   | Contains web files like `index.jsp` — the frontend of your web app.     |
| `index.jsp`         | Entry point of your web application.                                    |
| `pom.xml`           | Maven configuration file — used to build the WAR package.               |
| `Jenkinsfile`       | Defines CI/CD pipeline steps for Jenkins.                              |
| `deploy.yml`        | Ansible playbook — automates deployment tasks.                          |
| `inventory`         | Ansible inventory — lists target hosts (e.g., EC2 IPs).                 |



 🛠️ Required Tools on AWS EC2

 ### 1. Git
- **Purpose**: Version control and code management.
- **Install**:
  ```bash
  sudo apt update
  sudo apt install git -y
  ```

---

## 🚀 Jenkins and Java Installation Guide (Ubuntu 24.04 Noble)

This guide walks you through installing **OpenJDK 17** and **Jenkins** on Ubuntu 24.04, including fixing GPG key issues and enabling the Jenkins service.

---

### 🔧 Step 1: Install Java (OpenJDK 17)

Jenkins requires Java to run. Install OpenJDK 17:

```bash
sudo apt update
sudo apt install openjdk-17-jre -y
java --version
```

---

### 🔐 Step 2: Add Jenkins Repository and GPG Key

Fix the GPG key issue and add the Jenkins repository:

```bash
# Download the updated Jenkins GPG key
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key

# Add Jenkins repository
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] https://pkg.jenkins.io/debian-stable binary/" | \
  sudo tee /etc/apt/sources.list.d/jenkins.list > /dev/null
```

---

### 📦 Step 3: Install Jenkins

```bash
sudo apt update
sudo apt install jenkins -y
```

---

### ▶️ Step 4: Start and Enable Jenkins Service

```bash
sudo systemctl start jenkins
sudo systemctl enable jenkins
```

---

### 🌐 Step 5: Access Jenkins Web Interface

Open your browser and go to:

```
http://<your-server-ip>:8080
```

To retrieve the initial admin password:

```bash
sudo cat /var/lib/jenkins/secrets/initialAdminPassword
```

---

### 🔥 Optional: Allow Jenkins Port Through Firewall

If UFW is enabled:

```bash
sudo ufw allow 8080/tcp
sudo ufw enable
sudo ufw status
```

###  and inventory files.
- **Install**:
  ```bash
  sudo apt install ansible -y
  ```

### 3. Apache Tomcat
- **Purpose**: Host and run your Java web application (WAR file).
- **Install**:
  ```bash
  sudo apt install tomcat9 -y
  ```
🛠️ Apache Maven Installation (Ubuntu 24.04 Noble)
Apache Maven is required to build and manage your Java project (pom.xml).

🔧 Install Maven

✅ Verify Installation
```bash

sudo apt update
sudo apt install maven -
```

---

## 🔄 Deployment Flow

1. **Code Commit** → Git
2. **Build & Test** → Jenkins (uses `pom.xml`)
3. **Initialize Deployment** → Ansible (`deploy.yml`, `inventory`)
4. **Deploy Application** → Apache Tomcat (WAR file)

---

## ✅ Notes

- has internet access and security group rules allow necessary ports (e.g., 8080 for Tomcat, 8080/8081 for Jenkins).
- Add your EC2 IPs to the `inventory` file for Ansible to target them correctly.

