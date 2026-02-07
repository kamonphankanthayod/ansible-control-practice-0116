# Ansible Control Practice – CS365 (IaC)

**Student:** Kamonphan Kanthayod  
**Date:** Feb 6, 2026  

---

## Project Overview

This project demonstrates how to use **Ansible** as an Infrastructure as Code (IaC) tool to:

- Provision an EC2 instance on AWS
- Configure the instance automatically
- Deploy and run a Node.js web application

The goal is to show how configuration management can replace manual server setup.

---

## Architecture Diagram
```text
+------------------------+
|  Ansible Control       |
|  (AWS Cloud9)          |
+------------------------+
            |
            |  SSH + Ansible
            v
+------------------------+
|  AWS EC2               |
|  Amazon Linux 2023     |
|                        |
|  - Node.js             |
|  - Sample App          |
|  - Port 8080 Open      |
+------------------------+
            |
            |  HTTP
            v
         Browser
   http://<EC2-IP>:8080
```

---

## Project Structure
```text
ansible/
├── group_vars/
│ └── sample_app_ansible_0116.yml
├── roles/
│ └── sample-app/
│ ├── files/
│ │ └── app.js
│ └── tasks/
│ └── main.yml
├── configure_sample_app_playbook.yml
├── create_ec2_instances_playbook.yml
├── inventory.example.yml
├── smoke_test.yml
├── test_playbook.yml
└── .gitignore
```

---

## Technologies Used

- Ansible
- AWS EC2
- AWS Cloud9
- Node.js
- Amazon Linux 2023

---

## Usage

### 1) Create EC2 Instance
```bash
ansible-playbook create_ec2_instances_playbook.yml
```

### 2) Update inventory
Copy example and edit:
```bash
cp inventory.example.yml inventory.aws_ec2.yml
```
Replace with your EC2 public DNS.

### 3) Configure EC2
```bash
ansible-playbook -i inventory.aws_ec2.yml configure_sample_app_playbook.yml
```

---

## Result

Open in browser:
```text
http://<EC2-PUBLIC-IP>:8080
```
Expected output:
```text
Hello, World!
```

![Result Image](ansible_successed_result%20-%20Copy.png)

---

## Security

The following files are ignored:
- inventory.aws_ec2.yml
- *.key
- *.pem

These contain sensitive credentials and should not be committed.

---

## Learning Outcomes

- Understand Infrastructure as Code
- Automate server configuration
- Use Ansible roles and inventories
- Deploy a real application on cloud VM
