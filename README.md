
# 🟢 Scalable Web Application on AWS

This project demonstrates how to deploy a scalable and highly available web application using **EC2, Auto Scaling Group, ALB, IAM Roles, CloudWatch, and SNS** on AWS.

---

## 📐 Architecture

- **VPC** with public subnets
- **EC2 instances** with NGINX installed (via User Data)
- **Application Load Balancer (ALB)** to distribute traffic
- **Auto Scaling Group (ASG)** to maintain availability
- **IAM Role** attached to EC2 for secure AWS access
- **CloudWatch Alarms** to monitor CPU usage
- **SNS Notifications** via Email & SMS

---

## 🚀 Deployment Steps

### 1. Create a VPC and two public subnets

### 2. Launch two EC2 instances
- Use Amazon Linux 2
- Add the following User Data script:

```bash
#!/bin/bash
yum update -y
yum install -y nginx
systemctl start nginx
echo "<h1>Deployed from EC2 $(hostname)</h1>" > /usr/share/nginx/html/index.html
```

### 3. Create a Security Group
- Allow HTTP (80), SSH (22), and ALB access

### 4. Create ALB and target group
- Attach both instances

### 5. Create an Auto Scaling Group (ASG)
- Based on CPU threshold (e.g., >70%)

### 6. Setup IAM Role
- Attach `CloudWatchAgentServerPolicy` or custom policy

### 7. Configure CloudWatch Alarm & SNS
- Create alarm for CPU utilization
- Send email/SMS via SNS topic

---

## 📸 Screenshots

| Component         | Screenshot               |
|------------------|--------------------------|
| EC2 Instance      | `screenshots/ec2.png`     |
| CloudWatch Alarm  | `screenshots/alarm.png`   |

---

## ✅ Learning Outcomes

- Build scalable EC2 architecture with best practices
- Configure IAM Roles instead of access keys
- Monitor & alert using CloudWatch + SNS
- Understand ALB and Auto Scaling integration

---

## 🔒 Notes

- Make sure to **confirm SNS email** subscription
- Don’t expose ports other than 80/443 in production
