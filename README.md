
# 🚀 Scalable Web Application with ALB and Auto Scaling

This project demonstrates how to deploy a secure, highly available, and scalable web application on AWS using EC2 instances, Application Load Balancer (ALB), and Auto Scaling Groups (ASG). It follows AWS best practices for network design, compute management, monitoring, and cost optimization.

---

## 📦 Project Components

### ✅ 1. **VPC & Networking**
- Created a custom VPC with:
  - 2 Public Subnets (across different Availability Zones)
  - 2 Private Subnets (optional for DB layer)
  - Internet Gateway (IGW) attached to the VPC
  - Route tables for public access
- Ensured high availability by distributing instances across multiple AZs

---

### ✅ 2. **EC2 Instances**
- Launched two EC2 instances (Amazon Linux 2)
- Used `User Data` to auto-install and configure a simple web server:
  ```bash
  #!/bin/bash
  yum update -y
  yum install -y nginx
  systemctl start nginx
  systemctl enable nginx
  echo "<h1>Welcome to Yahya's Scalable Web App</h1>" > /usr/share/nginx/html/index.html
  ```

---

### ✅ 3. **Security Groups**
- Created security groups with:
  - Inbound HTTP (port 80) and SSH (port 22) access
  - Restricted access using specific IP ranges
- Assigned appropriate security groups to EC2 and ALB

---

### ✅ 4. **Application Load Balancer (ALB)**
- Deployed an ALB in public subnets
- Configured:
  - Target Group with EC2 instances
  - Health checks on port 80
- Used the ALB DNS name to access the app publicly

---

### ✅ 5. **Auto Scaling Group (ASG)**
- Created ASG with:
  - Launch template linked to our AMI/User Data
  - Minimum 2, Maximum 4 instances
  - Auto Scaling policies based on CPU utilization (>70%)
- Verified scaling by simulating high traffic

---

### ✅ 6. **Monitoring with CloudWatch**
- Enabled detailed monitoring on EC2 instances
- Created custom CloudWatch Alarms:
  - CPU Utilization > 70%
  - Sends alert via SNS

---

### ✅ 7. **Notifications with SNS**
- Created an SNS topic
- Subscribed email for notifications
- Verified alerts received when threshold exceeded

---

### ✅ 8. **IAM Roles**
- Created IAM Role with:
  - EC2 full access
  - CloudWatch access
- Attached role to EC2 for logging and monitoring permissions

---

## 📂 Folder Structure

```bash
📁 scalable-web-app/
├── launch-template.sh        # User data script for EC2
├── architecture-diagram.png  # AWS architecture diagram (if any)
├── screenshots/              # Key screenshots (optional)
└── README.md                 # This file
```

---

## 🧪 Testing

- Verified load balancing by refreshing ALB URL multiple times
- Simulated CPU load using `stress` to trigger scaling and alerts:
  ```bash
  sudo yum install -y stress
  stress --cpu 2 --timeout 120
  ```

---

## 🧾 Notes

- You must allow port 80 in the security group of both EC2 and ALB.
- DNS name of the ALB is used to access the web app.
- Auto Scaling will take a few minutes to launch new instances.
- Make sure instances are in **Healthy** status in the Target Group.

---

## 👨‍💻 Author

**Yahya Fayad**  
[GitHub](https://github.com/yahyafayad) | [LinkedIn](https://linkedin.com/in/yahyafayad)  
Email: yahyaifayad@gmail.com

---

## 📌 To Do (Optional Improvements)
- Use RDS in Private Subnet for DB layer (MySQL/PostgreSQL)
- Add HTTPS using ACM + ALB listener
- Implement CI/CD pipeline for auto-deployment
