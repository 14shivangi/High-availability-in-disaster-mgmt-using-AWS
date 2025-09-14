# High-availability-in-disaster-mgmt-using-AWS
High Availability Disaster Management project using AWS with multi-region failover, automated backups.

# Project Overview:
This project demonstrates how to design and implement a highly available disaster management system on AWS.
The goal is to ensure that critical applications (such as incident reporting, dashboards, and alerts) remain available and resilient, even in the event of infrastructure failures, natural disasters, or regional outages.

It uses multi-AZ and multi-region architecture, automated failover, data replication, and monitoring to achieve strong RTO (Recovery Time Objective) and RPO (Recovery Point Objective).

# Objectives:

Provide uninterrupted access to disaster management services.

Minimize downtime with high availability (HA).

Replicate critical data across regions for disaster recovery (DR).

Enable automated failover using AWS Route 53 and health checks.

Implement monitoring, backup, and cost-optimized infrastructure.

# Architecture:

High-level components:

Route 53 – DNS failover & health checks.

CloudFront – Low-latency content delivery & DDoS protection.

Application Load Balancer (ALB) – Distributes traffic across healthy instances.

Auto Scaling Group (ASG) – Automatically scales EC2 instances.

RDS / Aurora Global DB – Managed database with multi-AZ & cross-region replication.

S3 with Cross-Region Replication (CRR) – For storing and replicating disaster reports, files, and geo-data.

SNS & SQS – For reliable alerts and message queuing.

CloudWatch & CloudTrail – Monitoring, logging, and auditing.

IAM & KMS – Security, access control, and encryption.

📊 Architecture Diagram
flowchart TD
    A[Users / Field App] --> B[Route 53 DNS Failover]
    B --> C[CloudFront]
    C --> D[ALB - Region A]
    C --> E[ALB - Region B (DR Region)]
    D --> F[EC2 / ECS in ASG - Region A]
    E --> G[EC2 / ECS in ASG - Region B]
    F --> H[RDS Primary (Region A)]
    G --> I[RDS Read Replica (Region B)]
    H <--> I
    F --> J[S3 (Region A)]
    J --> K[S3 Replicated (Region B)]
    F --> L[SNS / SQS]
    L --> M[Subscribers / Notification Systems]

# Implementation Steps: 

VPC Setup – Create VPC, subnets (public/private), and security groups in at least 2 AZs.

Compute Layer – Deploy EC2/ECS with Auto Scaling and ALB.

Database Layer – Launch RDS (Aurora Global DB recommended) with cross-region replication.

Storage – Create S3 buckets with Cross-Region Replication (CRR) enabled.

Failover – Configure Route 53 with health checks and failover routing policy.

Monitoring – Set up CloudWatch alarms, CloudTrail logs, and SNS notifications.

Backup – Automate EBS snapshots and copy them to DR region.

Security – Enforce IAM least privilege, enable encryption (KMS), and set up AWS WAF/Shield.

Testing – Simulate failures (AZ outage, region failover) and validate RTO/RPO.

# Features: 
Multi-AZ and multi-region deployment.

Automated failover using Route 53.

Real-time monitoring with CloudWatch.

Data durability with S3 CRR and RDS replication.

Backup & restore strategy with snapshots.

Secure and cost-optimized design.

# Disaster Recovery Strategy:

Hot standby: Both regions active (higher cost, lowest RTO).

Warm standby: Minimal resources in DR region, scale up on failover.

Cold backup: Store data only, spin up resources on demand (lowest cost, higher RTO).

This project uses a Warm Standby DR approach to balance cost and availability.
