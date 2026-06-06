# Architecture

## Initial Architecture

```text
User Browser
     |
     | HTTP / SSH
     v
AWS Security Group
     |
     v
Amazon Linux EC2 Instance
     |
     +-- Apache HTTP Server
     +-- PHP Runtime
     +-- Local MariaDB Database
     +-- WordPress Application
```

The initial version deployed WordPress on a single Amazon Linux EC2 instance using a traditional LAMP stack.

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
  +--------+-------> Amazon EFS shared WordPress uploads
  |
  +---------------> Amazon RDS managed database
```

## Enhancement Purpose

### Route 53
Provides a stable DNS entry point so users access the service through a domain rather than a direct infrastructure endpoint.

### Application Load Balancer
Distributes traffic to healthy EC2 instances and helps prevent one failed instance from taking down the whole application.

### Auto Scaling Group
Automatically replaces unhealthy instances and supports scaling when demand changes.

### Amazon RDS
Moves the database away from the EC2 instance, reducing manual database administration and improving maintainability.

### Amazon EFS
Provides shared file storage for WordPress uploads so multiple EC2 instances can access the same media files.
