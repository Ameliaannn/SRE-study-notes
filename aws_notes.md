# AWS Basic Notes

## 1. AWS Account Management

The root account has full permissions and should only be used for account management tasks, such as changing passwords, enabling support plans, and closing the account. It is crucial to set a strong password and enable Multi-Factor Authentication (MFA). After setting up the account, create an IAM user for daily operations to avoid using the root account. AWS provides several support plans: Free, Developer, Business, and Enterprise. Account closure must be performed by the root user, and data backup is recommended before proceeding.

## 2. AWS Development History

Initially, companies had to build their own data centers by purchasing and maintaining physical servers. Later, colocation hosting allowed companies to place their servers in third-party data centers while managing them independently. Now, with AWS cloud computing, servers are virtualized, and resources can be purchased on-demand, making operations more flexible and efficient.

## 3. Core Service Concepts

### EC2 (Elastic Compute Cloud)

AWS's virtual server service supports elastic scaling through Auto Scaling. Instance types include T series (general-purpose, burstable like t2.micro), M series (standard general-purpose), C series (compute-optimized), R/X series (memory-optimized), and P/G series (GPU-powered).

### S3 (Simple Storage Service)

S3 is a cloud storage and backup repository designed for object storage with durability, security, and scalability. Dropbox was initially built on S3 and EC2.

## 4. AWS Shared Responsibility Model

AWS is responsible for data center physical security, hardware stability, and compliance certifications such as SOC, ISO, and PCI. Users are responsible for operating system updates, firewall and security group configurations, data backup and recovery, and securing applications from threats like SQL injection.

## 5. EC2 Hands-On Summary

To create an instance, choose an AMI (e.g., Ubuntu), select an instance type (e.g., t2.micro), create a key pair for SSH login, configure the security group to open ports 22 and 80, and launch the instance. Management involves connecting via browser-based SSH, updating the system with "sudo apt update && sudo apt upgrade," and installing a web server like Apache.

Auto Scaling allows CPU usage above 80% to trigger scaling out, and below 20% to scale in. Manual stop and start actions can migrate instances to other physical hosts. AMI snapshots enable quick deployment of new servers or backup recovery. EC2 cost optimization options include On-Demand instances (flexible but expensive), Reserved Instances (cheaper but inflexible), and Savings Plans (more flexible with moderate discounts).

## 6. AWS Networking and Security Basics

Security Groups act as virtual firewalls controlling inbound and outbound traffic. VPC (Virtual Private Cloud) provides an isolated network similar to a home LAN. Subnets divide VPCs into smaller segments: public subnets for web servers and private subnets for databases. NAT Gateway allows internal servers to access the Internet without exposure. Internet Gateway (IGW) connects VPC instances to the public Internet. Elastic IP provides fixed public IP addresses. VPN and Bastion Hosts ensure secure access to private instances.

## 7. Domain and Load Balancing

Route 53 enables binding Elastic IPs to domain names for resolution. Application Load Balancer (ALB) distributes traffic to multiple EC2 instances and requires setting up security group rules, target groups, and health checks.

## 8. Storage Optimization and Acceleration

Elastic Block Storage (EBS) provides virtual hard drives for EC2 instances, supporting snapshots, resizing, and reattachment. S3 Glacier offers low-cost cold storage for long-term archiving. S3 Lifecycle Management automates the transition of old files to Glacier or deletion. CloudFront accelerates content delivery globally, often paired with S3.

## 9. Access Control and Security Management

IAM users and roles should be used for daily tasks to avoid using the root account. IAM roles can be attached to EC2 instances for accessing AWS services like S3. AWS Secrets Manager securely stores sensitive information such as API keys and database credentials.

## 10. AWS Database Services

RDS (Relational Database Service) manages MySQL, PostgreSQL, SQL Server, and Oracle databases with automatic backups and high availability. DynamoDB is a high-performance NoSQL database suitable for real-time applications. ElastiCache provides Redis and Memcached services to accelerate database queries. SQS (Simple Queue Service) helps decouple application components through message queuing.

## 11. Deployment and Serverless Computing

Elastic Beanstalk allows developers to upload code and let AWS handle deployment and scaling. Lightsail offers simplified virtual servers ideal for beginners. ECS and EKS provide container services, with ECS being simpler and EKS offering Kubernetes-standard solutions. Lambda enables serverless function execution charged based on runtime.

## 12. Security Protection

WAF (Web Application Firewall) and Shield protect applications from common web attacks and DDoS attacks. GuardDuty monitors for abnormal behaviors. Inspector performs vulnerability scanning. Macie detects sensitive data exposure.

CloudTrail records all AWS account operations for auditing purposes. Security Hub centralizes security insights. Detective assists in investigating security incidents.

## 13. DevOps Related Services

Infrastructure as Code (IaC) tools like CloudFormation and Terraform automate AWS resource deployment. CloudWatch monitors system metrics and application logs. DevOps Guru provides intelligent anomaly detection. CodeGuru reviews code to find bugs and security risks.

