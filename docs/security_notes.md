# Security Notes

## Why the Raw Report Is Not Included
The original report contained lab credentials, database usernames/passwords, public IP screenshots, and AWS setup details. It is not suitable for public GitHub upload.

This repository uses a sanitized format:
- redacted screenshots
- placeholder credentials
- safe command references
- project explanation instead of raw report

## Improvements for a Real Deployment
If this was used in a real environment, the deployment should be improved with:

- IAM roles instead of long-term credentials
- Restricted SSH access to known IP addresses only
- HTTPS using TLS certificates
- Removal of `phpinfo.php` after testing
- Strong database passwords
- Regular security updates
- Backups or snapshots
- CloudWatch monitoring and logging
- Least-privilege database access

## Enhancement Security Considerations
- Route 53 and Load Balancer endpoints should be configured with HTTPS in a production setup.
- Security groups should restrict SSH access to trusted IP addresses.
- RDS credentials should be stored securely and never committed to GitHub.
- EFS access should be limited through correct security group and mount target configuration.
- Stress testing should be done only in authorised lab environments.
