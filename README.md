# High Availability Disaster Management System on AWS

## Overview:

This project demonstrates a **high availability and fault-tolerant architecture** for disaster management using AWS cloud services. It is designed to ensure continuity of critical disaster-response services during outages caused by natural disasters (floods, earthquakes) or technical failures (server outages).

The system leverages multi-region and multi-Availability Zone (AZ) deployments to maintain service availability, automatic failover, data replication, and continuous monitoring.

---

## Key Features
- **Multi-Region & Multi-AZ Deployment:** Distributes compute and database resources across multiple availability zones and geographic regions for fault tolerance.
- **Compute:** Uses EC2 instances deployed in multiple AZs and regions.
- **Database:** Amazon RDS with multi-AZ replication and automated backups for data durability.
- **Traffic Routing & Failover:** Amazon Route 53 DNS service to route traffic and perform health checks for automatic failover.
- **Load Balancing:** Elastic Load Balancers (ELB) distribute client requests across healthy EC2 instances.
- **Content Delivery:** Amazon CloudFront CDN for resilient and fast content delivery.
- **Backup & Monitoring:** Automated backups, CloudWatch monitoring, and alarms ensure service reliability.
- **Disaster Recovery Ready:** Keeps critical services like data ingestion, storage, web applications, and notifications operational during disasters.

---

## Architecture Diagram
(Include your architecture diagram here or link to an image file in the repo)

---

## AWS Services Used
- Amazon EC2
- Amazon RDS (Multi-AZ)
- Amazon Route 53
- Elastic Load Balancer (ALB/ELB)

---

## Setup & Deployment

### Prerequisites
- AWS Account with necessary permissions
- AWS CLI installed and configured
 
### Steps
1. **Create VPCs** in multiple regions with subnets in multiple AZs.
2. **Launch EC2 instances** in each region/AZ for application servers.
3. **Set up Amazon RDS** multi-AZ instance for database with automated backup.
4. **Configure Route 53** with health checks and failover routing policies.
5. **Deploy Elastic Load Balancers** in front of EC2 instances per region.
6. **Set up CloudFront** distribution for your web application.
7. **Enable CloudWatch** monitoring and configure alarms.
8. **Implement automated backups and failover** testing.

---

## Usage
- Access the disaster management application via the CloudFront URL.
- Route 53 ensures that traffic is sent to healthy endpoints automatically.
- In the event of failures in one region/AZ, traffic is redirected without downtime.

