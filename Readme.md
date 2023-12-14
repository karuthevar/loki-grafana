# Nginx Promtail Loki Grafana on Amazon EC2 Linux 2 Stack on AWS CloudFormation

## Overview
This AWS CloudFormation stack deploys a Nginx Promtail Loki Grafana on Amazon EC2 Linux 2 (Promtail, Nginx, Loki, Grafana) environment on an Amazon EC2 instance. It includes configurations for Amazon Linux 2, SSM Session Manager, and S3 storage for Loki.

## Prerequisites
- AWS account with permissions to create EC2 instances, S3 buckets, IAM roles, and Security Groups.
- An existing S3 bucket or the stack will create a new one.

## Stack Details
- **EC2 Instance**: Runs Amazon Linux 2 and hosts the Nginx Promtail Loki Grafana on Amazon EC2 Linux 2 stack.
- **Security Group**: Configured to enable HTTP and HTTPS traffic.
- **S3 Bucket**: Used for Loki's log storage.
- **IAM Roles**: Necessary permissions for EC2 instances and S3 access.
- **UserData Script**: Automates the setup for Promtail, Nginx, Loki, and Grafana.

## Parameters
- `BucketName`: Name of the S3 bucket for Loki storage.
- `LokiRegion`: AWS region for the backend S3 bucket for Loki.
- `LokiUsername`: Username for Loki.
- `LokiPassword`: Password for Loki (HTTP Basic Authentication).
- `GrafanaUsername`: Username for Grafana login.
- `GrafanaPassword`: Password for Grafana login.
- `LatestAmiId`: Amazon Linux 2 AMI ID (automatically resolved).

## Outputs
- `InstanceId`: The ID of the created EC2 instance.
- `PublicIp`: The public IP address of the EC2 instance.
- `LokiS3Bucket`: The S3 bucket used for Loki's storage.
- `LokiEndPoint`: The endpoint for Promtail to push logs to Loki.
- `GrafanaEndpoint`: The endpoint to access Grafana.
- `InstanceDNSName`: DNS name of the EC2 instance.

## Deployment Steps
1. Log in to your AWS Console and navigate to the CloudFormation service.
2. Create a new stack and upload this template.
3. Fill in the parameters as required.
4. Review and launch the stack.
5. Once the stack creation is complete, access the EC2 instance's public IP to use Grafana, Loki, and Nginx.

## Accessing the Services
- **Grafana**: Accessible at `https://${PublicIp}:3000`.
- **Loki**: Integrated with Grafana for log management.
- **Nginx**: Serving as a reverse proxy for Loki and Grafana.

## Security Considerations
- The stack uses self-signed SSL certificates for HTTPS. For production environments, replace these with valid certificates.
- Default ports are open for HTTP and HTTPS; consider restricting access based on your network policies.
- Regularly update your AMI for security patches.

## Customization
You can customize the stack by modifying the CloudFormation template. Ensure to update UserData scripts for any major changes.

---

*Note: This template and instructions are provided 'as is' and should be tested in a non-production environment before use.*
