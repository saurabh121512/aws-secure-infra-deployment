# aws-secure-infra-deployment

# AWS Secure & Highly Available Infrastructure Deployment

## Architecture Diagram
![AWS Architecture](architecture.png)

## Overview
This project demonstrates a secure, highly available, and performance-optimized AWS production architecture deployed in the Mumbai (ap-south-1) region. Initially built to establish standard enterprise-grade security controls, the infrastructure was subsequently upgraded to resolve a real-world production bottleneck where the application layer consistently exceeded 87% daily CPU utilization.

---

## 🚀 Performance Optimization Case Study

### The Challenge: Infrastructure Strain (87%+ Workload)
The original deployment experienced performance degradation under a sustained traffic surge, causing compute nodes to consistently operate above **87% daily CPU utilization**. This led to:
* **Response Latency:** High CPU saturation delayed page rendering and runtime code execution.
* **MySQL Query Queuing:** Compute bottlenecks restricted data processing speeds, leading to thread contention and cascading database query queues.
* **Storage Bottlenecks:** Heavy transactional traffic choked standard disk throughput limits, resulting in severe I/O wait times.

### The Solution: 6th-Gen AMD Architecture Upgrade
To systematically fix these performance issues while optimizing operational expenditure, I proposed and executed a migration strategy shifting the compute tier to **AWS M6a and C6a instances** powered by **3rd Gen AMD EPYC processors**.

### Real-World Architectural Impact
* **Compute Acceleration:** Upgraded to a 3.6 GHz all-core turbo frequency, drastically lowering baseline CPU utilization and restoring snappy application response times.
* **Network & Storage Expansion:** Scaled network bandwidth up to **50 Gbps** at the load balancer layer and dedicated EBS bandwidth up to **40 Gbps**, completely eliminating MySQL storage I/O bottlenecks.
* **Price-Performance Gains:** Leveraged AMD's pricing model to achieve up to a **35% price-performance improvement**, enabling cost-effective capacity scaling via AWS Auto Scaling.

---

## 🛠️ Key Components
* **Route 53:** Global DNS routing and domain mapping.
* **AWS WAF (Web Application Firewall):** Layer 7 protection safeguarding the front-end against common web exploits.
* **Application Load Balancer (ALB):** Distributed incoming traffic across multiple availability zones.
* **VPC Architecture:** Configured isolated public and private subnet topographies.
* **EC2 Instances (M6a / C6a):** High-performance, Nitro-powered compute instances hosting the application layer.
* **NAT Gateway:** Enabled secure, outbound-only internet connectivity for private resources.
* **OpenVPN:** Established a secure, encrypted administrative tunnel to access internal resources.
* **MySQL Database:** Relational database securely siloed in the isolated database private subnet tier.
* **IAM, S3, & CloudWatch:** Orchestrated least-privilege identity access management, secure object storage, and proactive performance monitoring/logging.

---

## 🔒 Security & Availability Matrix
* **Layered Network Isolation:** Strict private subnet segregation ensures that the core application and MySQL database layers are completely hidden from the public internet.
* **Least-Privilege Security Posture:** Explicit IAM policies and tight EC2 Security Groups ensure only verified network traffic can communicate between layers.
* **High Availability Architecture:** Leveraged multi-AZ redundancy via the ALB, coupled with AWS Auto Scaling, to deliver automated, self-healing infrastructure resilience.
