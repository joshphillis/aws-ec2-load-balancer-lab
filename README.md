# aws-ec2-load-balancer-lab

# 🌐 High-Availability Web Server Deployment on AWS with ALB

This project demonstrates how to deploy two EC2-based HTTP servers across multiple availability zones behind an Application Load Balancer (ALB) using AWS. It includes health checks, sticky sessions, and full lifecycle management.

## 🚀 Project Overview

- Launches two EC2 instances in different AZs
- Installs a basic HTTP server on each instance
- Creates a security group allowing SSH and HTTP
- Configures an Application Load Balancer with:
  - Health checks on `/health.html`
  - Sticky sessions (session affinity)
- Demonstrates load balancing and failover
- Cleans up all resources after testing

## 🧰 Tools & Technologies

- AWS EC2 (t2.micro)
- Ubuntu Server 22.04 LTS
- Application Load Balancer (ALB)
- Target Groups
- Security Groups
- Sticky Sessions

## 🛠️ Deployment Steps

### 1. Launch EC2 Instances

- AMI: `ami-06d5e0de6baf595ca` (Ubuntu 22.04 LTS)
- Instance Names: `httpserver1`, `httpserver2`
- Key Pair: `pgpcc-key1`
- Subnets: `us-east-1a` and `us-east-1b`
- Security Group: `tio2-sg`
  - SSH (Port 22) from Anywhere
  - HTTP (Port 80) from Anywhere

### 2. Configure HTTP Servers

- Install Apache or Nginx
- Create a `health.html` file in `/var/www/html/`
- Ensure the HTTP page is accessible via public IP

### 3. Create Target Group

- Name: `web-tg`
- Target type: Instance
- Health check path: `/health.html`
- Healthy threshold: 2
- Register both instances

### 4. Create Application Load Balancer

- Name: `web-lb`
- Type: Application Load Balancer
- Network mapping: All AZs
- Security group: `tio2-sg`
- Listener: HTTP (Port 80) → Target group `web-tg`

### 5. Enable Sticky Sessions (Optional)

- Navigate to Target Group → Attributes → Edit
- Enable stickiness
- Set duration (e.g., 300 seconds)

### 6. Test Load Balancer

- Copy ALB DNS name (e.g., `web-lb-xxxx.elb.amazonaws.com`)
- Paste into browser: `http://<ALB-DNS>`
- Refresh multiple times to observe load balancing
- Sticky sessions will keep you on the same instance

### 7. Cleanup

```bash
# In AWS Console:
- Delete Load Balancer
- Delete Target Group
- Terminate both EC2 instances
```

## 🧪 Troubleshooting

- Ensure security group allows inbound HTTP
- Confirm health check file exists and is accessible
- Wait for ALB to pass health checks before testing

## 🧠 Author

**Joshua [Your Last Name]**  
Cloud Engineer | AWS & Azure Certified  
[LinkedIn](https://www.linkedin.com/in/YOUR-LINKEDIN) • [GitHub](https://github.com/YOUR_USERNAME)

---

## 📌 License

This project is for educational purposes and demonstrates AWS infrastructure concepts.

