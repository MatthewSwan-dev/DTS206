# DTS206 – Secure Clinical Cloud Infrastructure

## Overview

This repository contains the implementation, configuration files and supporting evidence for the DTS206 Virtualisation and Infrastructure assignment.

The project is based on a fictional healthcare organisation, MediCore Health Systems, responsible for storing and processing sensitive patient information. The objective was to design, deploy and secure a cloud-based infrastructure capable of supporting healthcare workloads while adhering to security principles aligned with GDPR requirements and recognised industry best practices.

The solution was implemented using AWS cloud services, Linux administration, containerisation technologies and Kubernetes orchestration. Security monitoring, vulnerability assessment and access control mechanisms were incorporated throughout the project to strengthen the overall security posture of the environment.

---

## Architecture Overview

The environment was deployed within a custom Amazon Virtual Private Cloud (VPC) using a three-tier network architecture. This approach separates public-facing services from application and database resources, reducing unnecessary exposure and improving security.

### Core Components

- Application Load Balancer (ALB)
- Bastion Host
- Web/Application Server
- Database Server
- Amazon RDS PostgreSQL
- Amazon S3 Storage
- Amazon CloudWatch
- Auto Scaling Group
- IAM Roles and Policies

### Network Design

#### Public Subnet

- Bastion Host
- Application Load Balancer

#### Private Subnet

- Web/Application Server
- Application Services

#### Restricted Subnet

- Database Resources
- Amazon RDS PostgreSQL

This layered network design ensures that critical systems remain isolated from direct internet access while allowing controlled communication between infrastructure components.

---

## Deployment Process

### AWS Infrastructure

The following infrastructure components were designed, deployed and configured:

1. Created a custom VPC.
2. Configured public, private and restricted subnets.
3. Created route tables and internet gateway connectivity.
4. Deployed and secured a bastion host for administrative access.
5. Deployed the application server.
6. Configured database services.
7. Implemented security groups and network access controls.
8. Created an Amazon S3 bucket for secure storage.
9. Deployed an Amazon RDS PostgreSQL instance.
10. Configured IAM roles and permissions.
11. Implemented CloudWatch monitoring and alerting.
12. Configured an Application Load Balancer.
13. Implemented Auto Scaling to improve availability and resilience.

### Containerisation and Orchestration

Container technologies were used to deploy and manage application workloads.

1. Built a Docker image.
2. Created and tested a Docker Compose deployment.
3. Performed vulnerability assessments using Trivy.
4. Performed vulnerability assessments using Grype.
5. Deployed workloads to a Kubernetes (K3s) cluster.
6. Verified Kubernetes self-healing capabilities by simulating container failure and observing automatic pod recreation.

---

## Security Controls Implemented

The following security controls were incorporated into the solution:

- Network segmentation through subnet design.
- Security groups configured using least-privilege principles.
- Role-based access control through AWS IAM.
- Secure administrative access through a bastion host.
- Vulnerability assessment using Trivy and Grype.
- Vulnerability remediation based on scan findings.
- Centralised monitoring through Amazon CloudWatch.
- CloudWatch alarms for infrastructure monitoring and alerting.
- Restricted database access within private network segments.
- Kubernetes self-healing and workload resilience features.

---

## Technologies Used

| Technology | Purpose |
|------------|---------|
| AWS | Cloud infrastructure platform |
| Ubuntu Linux | Server operating system |
| Docker | Containerisation |
| K3s Kubernetes | Container orchestration |
| Trivy | Container vulnerability scanning |
| Grype | Container vulnerability scanning |
| Python | Data analysis and visualisation |
| GitHub | Version control and repository management |

---

## Security References

- AWS Security Best Practices
- National Cyber Security Centre (NCSC) Cloud Security Guidance
- OWASP Container Security Guidance
- GDPR Security Principles

---

## Repository Structure

```text
analysis/
docker/
infrastructure/
kubernetes/
reports/
screenshots/
README.md
