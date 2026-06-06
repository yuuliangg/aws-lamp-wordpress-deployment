# Cloud Architecture Enhancements

This document describes the extended AWS architecture enhancements added after the initial EC2 LAMP and WordPress deployment.

The original deployment used a single Amazon Linux EC2 instance running Apache, PHP, MariaDB, and WordPress. The enhancement improves the architecture by adding fault tolerance, automatic scaling, managed database services, and shared file storage.

## Enhancement 1: Fault Tolerance

### Services Used
- Amazon Route 53
- Application Load Balancer
- Auto Scaling Group

### Purpose
Route 53 provides a stable DNS entry point for users, while the load balancer distributes traffic across healthy instances. If one instance fails, the load balancer stops sending traffic to it and the Auto Scaling Group can launch a replacement instance.

### Why This Matters
A single EC2 instance creates a single point of failure. By adding DNS routing, load balancing, and automatic replacement, the application becomes more resilient and can continue serving users even when an individual instance fails.

## Enhancement 2: Automatic Demand Handling

### Services Used
- Auto Scaling Group
- Application Load Balancer
- ApacheBench stress testing

### Purpose
Auto Scaling helps the system respond to changes in traffic demand automatically. When traffic increases, additional instances can be launched. When traffic decreases, capacity can be reduced.

### Testing Method
A stress test was performed using ApacheBench:

```bash
ab -t 120 -c 200 http://wordpress.internal/wordpress/
```

This simulates concurrent traffic to test whether the architecture can handle increased load and whether replacement/scaling behaviour works as intended.

## Enhancement 3: Reduced Administrative Tasks

### Services Used
- Amazon RDS
- Amazon EFS

### RDS Purpose
The local MariaDB database was replaced with Amazon RDS to reduce manual database administration. Instead of managing the database service directly on the EC2 instance, RDS handles many operational tasks such as database hosting, maintenance, and reliability features.

A validation step involved stopping the local MariaDB service and refreshing WordPress to confirm that WordPress could continue using the external database layer.

```bash
sudo systemctl stop mariadb
```

### EFS Purpose
Amazon EFS was used as shared file storage for WordPress uploads. This allows multiple WordPress instances to access the same uploaded media files, which is important when the application is running behind a load balancer with multiple EC2 instances.

Example validation commands:

```bash
ls /mnt/efs/wp-content/uploads
ls /mnt/efs/wp-content/uploads/2026/02
```

## Enhanced Architecture Summary

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

## Key Learning Points
- A single-server deployment is simple but fragile.
- Load balancers and Auto Scaling improve availability and demand handling.
- RDS reduces manual database management.
- EFS allows shared WordPress media storage across multiple instances.
- Stress testing helps validate whether the architecture responds properly under load.
