# aws-ec2-load-balancer-lab

# 🌐 High-Availability Web Server Deployment on AWS with ALB

# ⚙️ AWS Load Balancer Demo — EC2 Target Groups & Sticky Sessions

## Overview  
This project demonstrates deploying an **Application Load Balancer (ALB)** in **AWS** to distribute traffic across two EC2 instances in separate availability zones. It includes security group setup, target group configuration with health checks, and an exploration of sticky session behavior — providing hands-on experience with scalable and stateful cloud infrastructure design.

## 🛠️ Technologies Used
- **Amazon EC2** – Virtual instance provisioning  
- **Application Load Balancer (ALB)** – Traffic distribution & session persistence  
- **Target Groups** – Instance registration and health monitoring  
- **Security Groups** – Configured for HTTP (80) and SSH (22) access  
- **AWS Console** – Visual deployment and configuration  
- **PEM Key Pair (xxxxxx)** – SSH access to instances

## 🧩 Deployment Steps
1. **Launch EC2 Instances**  
   - Deployed `httpserver1` in `us-east-1a` and `httpserver2` in `us-east-1b`  
   - Used `ami-06d5e0de6baf595ca` for both  
   - Applied shared security group (`tio2-sg`) allowing SSH & HTTP traffic

2. **Create Target Group (`web-tg`)**  
   - Set target type: Instances  
   - Health check path: `/health.html`  
   - Adjusted healthy threshold: `2`  
   - Registered both EC2 instances

3. **Configure Application Load Balancer (`web-lb`)**  
   - Enabled across all availability zones  
   - Linked to `xxxx-sg` for security  
   - Default action: Forward to `web-tg`  
   - Verified traffic alternated between both instances via DNS

4. **Enable Sticky Sessions (Bonus)**  
   - Activated session affinity on `web-tg`  
   - Validated consistent routing to the same instance across browser refreshes

## 🔍 Test & Validation
- Accessed instances via public IPs to confirm HTTP responses  
- Used ALB DNS (`web-lb-xxxxxxxx.us-east-1.elb.amazonaws.com`) to test traffic distribution  
- Observed round-robin behavior and sticky session persistence  
- Performed full teardown: deleted load balancer, target group, and terminated EC2 instances

## ✅ Outcomes
- Demonstrated cross-AZ deployment using ALB  
- Explored health check mechanics and traffic failover  
- Implemented session stickiness for stateful client routing  
- Practiced full resource lifecycle: deployment → testing → cleanup


## 📌 License

This project is for educational purposes and demonstrates AWS infrastructure concepts.

