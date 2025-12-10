# Project #1 — AWS VPC + Public Subnet + EC2 Web Server

This project demonstrates how to deploy a basic web server running on an EC2 instance inside a custom VPC with a public subnet.  
It covers the essential cloud networking components used in real Cloud Support / Cloud Operations roles.

---

## 📌 Architecture Diagram

Internet  
   |  
[ Internet Gateway ]  
   |  
[VPC: 10.0.0.0/16]  
   |  
[ Public Subnet: 10.0.1.0/24 ]  
   |  
[ EC2 Web Server (Amazon Linux) ]  
- Public IP: 13.57.16.92  
- Security Group:  
  - SSH (22) from My IP  
  - HTTP (80) from 0.0.0.0/0  

---

## 📌 Components Used

| Component | Description |
|----------|-------------|
| **VPC (10.0.0.0/16)** | Custom virtual private network |
| **Public Subnet (10.0.1.0/24)** | Subnet with route to Internet Gateway |
| **Internet Gateway** | Enables internet access for EC2 |
| **Route Table** | Routes 0.0.0.0/0 → IGW |
| **EC2 Instance** | Amazon Linux web server |
| **Security Group** | Allows HTTP (80) & SSH (22) |
| **Apache (httpd)** | Web server software |

---

## 📌 Deployment Steps

### 1. Create VPC
- CIDR: `10.0.0.0/16`
- Name: `trainingVPC`

### 2. Create Public Subnet
- CIDR: `10.0.1.0/24`
- Name: `public-subnet-1`
- AZ: Any

### 3. Create & Attach Internet Gateway
- Name: `training-igw`
- Attach to VPC

### 4. Route Table
- Add route: `0.0.0.0/0 → Internet Gateway`
- Associate with public-subnet-1

### 5. Launch EC2 Instance
- AMI: Amazon Linux 2 or 2023
- Instance type: `t2.micro`
- Subnet: public-subnet-1
- Auto-assign Public IP: Enabled
- Security Group:
  - SSH (22) from My IP
  - HTTP (80) from anywhere

### 6. Install Apache Web Server

```bash
sudo dnf update -y
sudo dnf install -y httpd
sudo systemctl enable httpd
sudo systemctl start httpd
7. Create Test Webpage
bash
Copy code
echo "<h1>Hello from my first AWS web server</h1>" | sudo tee /var/www/html/index.html
8. Test in Browser
Visit:

cpp
Copy code
http://13.57.16.92
Expected result:

Hello from my first AWS web server

📸 Screenshots
VPC


Subnet


Internet Gateway


Route Table


EC2 Instance


Security Group Rules


Browser Result


📌 Troubleshooting Notes
1. Browser cannot connect
Missing port 80 in Security Group

Apache service not running

Wrong public IP

Route table not associated with subnet

2. SSH not working
Port 22 not open to your IP

Key file permissions wrong

Wrong username (ec2-user)

3. Webpage not updating
Browser cache

Wrong file path (/var/www/html/index.html)

✅ Result
This project demonstrates:
✔ Building foundational AWS networking
✔ Deploying an EC2-based web server
✔ Understanding routing, gateways, and security groups
✔ Real Cloud Support / Cloud Ops skills
