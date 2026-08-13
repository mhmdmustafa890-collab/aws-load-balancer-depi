# aws-load-balancer-depi 

> *Project Overview:* A highly available, secure, and fault-tolerant AWS web architecture featuring a custom VPC, Public Subnets, EC2 Web Servers with automated Apache installation via User Data, and an Application Load Balancer.

> ![project](https://github.com/user-attachments/assets/b47559f5-d5d4-436d-b718-ab71ff79e3f8)


---

## 1. VPC and Internet Connectivity Setup
* Created a Virtual Private Cloud (VPC) with the CIDR block 10.0.0.0/16.
* Attached an Internet Gateway (igw-0a1b2c3d4e5f6g7h8) to the VPC to enable external internet access.

> ![VPC Setup](https://github.com/user-attachments/assets/d5f4242e-b201-4343-9841-fd46d5c06dcd)

---

## 2. Subnet Configuration
* *Public Subnet 1:* Deployed in Availability Zone us-east-1a with CIDR 10.0.1.0/24.
* *Public Subnet 2:* Deployed in Availability Zone us-east-1b with CIDR 10.0.2.0/24.

> ![Subnets Setup](https://github.com/user-attachments/assets/52569300-30c7-4f2f-a929-dedb69184c21)

---

## 3. Route Table Configuration
* Created a public route table (rtb-070921f6acddbeffe) associated with both public subnets.
* Configured local routing (10.0.0.0/16 -> local) and internet routing (0.0.0.0/0 -> Internet Gateway).

> ![Route Table Setup](https://github.com/user-attachments/assets/e1d0ff90-eb21-476d-bb8c-c4c0e6c30356)

---

## 4. Security Groups Setup
* *Load Balancer SG (alb-sg):* Allowed inbound HTTP (port 80) from anywhere (0.0.0.0/0).
* *Web Server SG (web-sg):* 
  * Allowed HTTP exclusively from alb-sg.
  * Allowed SSH (port 22) for remote management from a trusted IP (My IP).

> ![Security Groups Setup](https://github.com/user-attachments/assets/44dc53cf-b5c6-4c48-988e-1ff4e52b30ee)

---

## 5. EC2 Instances & User Data Configuration
* *Web Server 1:* Launched in us-east-1a (Private IP: 10.0.1.10, Public IP: 54.226.11.101) with User Data running Apache and a custom greeting message.
* *Web Server 2:* Launched in us-east-1b (Private IP: 10.0.2.10, Public IP: 3.87.45.210) with User Data running Apache and a custom greeting message.

> ![EC2 Instances](https://github.com/user-attachments/assets/bca1a417-aa04-44a1-ba09-41c4004e7825)

---
## 6. WSL Ubuntu and Apache Server Setup
* Set up the local development environment using Windows Subsystem for Linux (WSL).
* Installed the Apache web server within the Ubuntu environment.
* Created an index.html file with a custom greeting message and verified local access.

> ![WSL Ubuntu Setup](https://github.com/user-attachments/assets/6eadfb36-f902-4e3d-84e5-33fda356d7bf)
> ![WSL Ubuntu Setup](https://github.com/user-attachments/assets/8a767d52-7055-408b-bcbd-47a25ee92aac)
> ![WSL Ubuntu Setup](https://github.com/user-attachments/assets/db74c4ed-0b8f-473b-a8ff-94273208c16f)

---

## 7. Application Load Balancer & High Availability Testing
* Created a Target Group (web-tg) using HTTP on port 80 with health checks enabled.
* Configured an Application Load Balancer to distribute traffic between the two web servers.

> ![Load Balancer Architecture](https://github.com/user-attachments/assets/f732867e-7ea5-46fb-9bf2-7a78fccd8143)
> ![Target group](https://github.com/user-attachments/assets/d7e11873-fc92-4a1f-9df3-703ee723463d)
---

## 8. Final Project Results
* Accessed the Application Load Balancer using the DNS Name.
* Verified that traffic is distributed between the two web servers.
* Confirmed that refreshing the browser switches the response between Web Server 1 and Web Server 2.
* Tested high availability by stopping one server, confirming the Load Balancer automatically routed all traffic to the remaining healthy server.
* Verified that stopping both servers resulted in an error page due to the absence of healthy targets.

> ![Server_1_open_Server_2_close](https://github.com/user-attachments/assets/40a25f22-7781-44e5-a393-bfebd51c503b)
> ![Server_2_open_Server_1_close](https://github.com/user-attachments/assets/c55a3a92-93f6-4c1c-ad56-92be518716ac)
> ![Server_2_close_Server_1_close](https://github.com/user-attachments/assets/8e9f9086-0cb7-4a0f-9ac1-18293b2b3f8d)













