
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

### 2. Java (Required for Jenkins)
- **Purpose**: Jenkins is a Java-based application.
- **Install**:
  ```bash
  sudo apt install openjdk-11-jdk -y
  ```

### 3. Jenkins
- **Purpose**: Automate build and test processes.
- **Install**:
  ```bash
  wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -
  sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'
  sudo apt update
  sudo apt install jenkins -y
  sudo systemctl start jenkins
  sudo systemctl enable jenkins
  ```

###  and inventory files.
- **Install**:
  ```bash
  sudo apt install ansible -y
  ```

### 5. Apache Tomcat
- **Purpose**: Host and run your Java web application (WAR file).
- **Install**:
  ```bash
  sudo apt install tomcat9 -y
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

