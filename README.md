# AWS LAMP & WordPress Deployment with Cloud Architecture Enhancements

## Overview
This project documents a cloud migration proof-of-concept using Amazon Web Services. The initial deployment configured an Amazon Linux EC2 instance as a web hosting environment with Apache HTTP Server, MariaDB, PHP, and WordPress.

The enhanced version extends the architecture with Route 53, an Application Load Balancer, Auto Scaling, Amazon RDS, and Amazon EFS to improve fault tolerance, scalability, database management, and shared file storage.

## Problem Statement
A small company wanted to explore whether selected web services could be hosted on AWS instead of relying entirely on an on-premises setup. The goal was to validate both:

1. A basic cloud-hosted WordPress deployment.
2. An improved architecture that can better handle failure, demand changes, and administrative workload.

## Tools and Technologies
- AWS EC2
- Amazon Linux
- Elastic IP
- Security Groups
- Apache HTTP Server
- MariaDB
- PHP
- WordPress
- SSH / PuTTY
- Route 53
- Application Load Balancer
- Auto Scaling Group
- Amazon RDS
- Amazon EFS
- ApacheBench

## Initial Deployment Features
- Created and configured an Amazon Linux EC2 instance
- Allocated and associated an Elastic IP
- Configured security group rules for HTTP and SSH access
- Installed and enabled Apache HTTP Server, MariaDB, PHP, and required dependencies
- Secured the MariaDB installation and created a WordPress database user
- Deployed WordPress on the EC2-hosted LAMP environment
- Validated PHP and web server functionality using browser-based testing
- Connected to the instance using SSH / PuTTY

## Cloud Architecture Enhancements

### Fault Tolerance
Route 53 and an Application Load Balancer were used to provide a stable access point and route traffic away from failed instances. Auto Scaling supports automatic instance replacement.

### Automatic Demand Handling
An Auto Scaling Group and Load Balancer were used to handle traffic changes. ApacheBench was used to generate test load and validate behaviour under demand.

### Reduced Administrative Tasks
Amazon RDS was introduced to move database management away from the EC2 instance. Amazon EFS was used to provide shared WordPress upload storage across instances.

## Enhanced Architecture

```text
Users
  |
  v
Route 53 DNS
  |
  v
Application Load Balancer
  |
  v
Auto Scaling Group
  |        |
  v        v
EC2 WordPress Instance(s)
  |        |
  +--------+-------> Amazon EFS shared uploads
  |
  +---------------> Amazon RDS managed database
```

## Security and Privacy Notes
The original school report contained lab passwords, public IP screenshots, and setup details. This public repository intentionally excludes the raw DOCX report and replaces it with a sanitized case study, redacted screenshots, and safe command references.

Do not commit:
- real AWS credentials
- key pair files
- passwords
- public IP addresses from active instances
- screenshots containing account identifiers

## Repository Structure
```text
aws-lamp-wordpress-deployment/
├── README.md
├── screenshots/
│   ├── initial deployment screenshots
│   └── enhancements/
│       └── enhancement evidence screenshots
├── docs/
│   ├── commands_reference.md
│   ├── enhancements.md
│   ├── resume_bullets.md
│   └── security_notes.md
├── report/
│   ├── aws-lamp-wordpress-case-study.pdf
│   └── README.md
└── architecture/
    └── architecture.md
```

## What I Learned
This project strengthened my understanding of both basic cloud deployment and improved cloud architecture design. The initial setup gave hands-on experience with EC2, Linux, LAMP, and WordPress deployment, while the enhancement introduced higher-level cloud architecture concepts such as fault tolerance, load balancing, Auto Scaling, managed databases, and shared storage.
