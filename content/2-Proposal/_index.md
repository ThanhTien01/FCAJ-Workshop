---
title: "Proposal"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---
# High Availability on AWS
## Ensuring High Availability on AWS

## 1. Problem Summary

In web applications, relying on a single server or a single Availability Zone can lead to service interruptions when the server experiences failures, traffic spikes, or infrastructure issues.

This workshop proposes building a web application on AWS using a High Availability model, where the application is deployed across multiple Amazon EC2 instances in different Availability Zones. An Application Load Balancer is used to distribute traffic, Auto Scaling ensures automatic scaling and replacement of servers when needed, Amazon RDS Multi-AZ provides database redundancy, and Amazon CloudWatch is used for system monitoring.

The goal of this workshop is to build a system that can maintain operations, tolerate failures, and automatically recover when a component in the system fails.

## 2. Problem Statement

If a web application is deployed on only one EC2 instance, it will have a Single Point of Failure. When the EC2 instance fails, the entire application may become inaccessible.

In addition, when traffic increases suddenly, a single server may not be able to handle the load. Scaling servers manually also increases response time and administrative workload.

For the database, if only one database instance is used, a database failure can also disrupt the entire application.

Therefore, this workshop focuses on addressing the following issues:

- Eliminate the Single Point of Failure at the application layer.
- Ensure the application continues to work when an EC2 instance fails.
- Automatically scale the system when traffic increases.
- Automatically replace failed EC2 instances.
- Improve database availability.
- Monitor and detect system issues.

## 3. Solution Architecture

The solution is built on AWS using a deployment model across two Availability Zones.

**Architecture diagram is missing**

| Component | Role |
|---|---|
| Amazon VPC | Builds the network environment |
| Public/Private Subnet | Separates network resources |
| EC2 | Runs the Python application |
| Docker | Packages the application |
| Amazon ECR | Stores Docker Images |
| Application Load Balancer | Distributes traffic |
| Auto Scaling | Automatically scales and replaces EC2 instances |
| Amazon RDS Multi-AZ | Provides database redundancy |
| CloudWatch | Monitoring and alerts |

Main workflow:
```text
User
↓
Application Load Balancer
↓
EC2 in AZ-A / EC2 in AZ-B
↓
Application
↓
RDS Multi-AZ
```

## 4. Technical Deployment

*Main implementation steps:*
1. Design a suitable VPC, subnets, security groups, and IAM roles.
2. Deploy EC2 instances running the Python application.
3. Create and configure the Application Load Balancer and target group.
4. Configure the Auto Scaling Group with scale-out and scale-in policies based on CPU or request volume.
5. Deploy Amazon RDS for the database and configure backups and maintenance.
6. Use Amazon S3 to store static content and backup data.
7. Set up CloudWatch metrics, alarms, and logs to monitor CPU, latency, and error rate.
8. Test failover by stopping one EC2 instance and observing ALB/ASG behavior.

## 5. Implementation Timeline and Milestones

| Week | Content | Result |
|---|---|---|
| Week 1 | Learn High Availability and AWS services | Understand the foundational knowledge |
| Week 2 | Design the Multi-AZ architecture | Complete system architecture |
| Week 3 | Prepare Python, Docker, and ECR | Application runs with Docker |
| Week 4 | Build VPC, EC2, and RDS | Basic system is operational |
| Week 5 | Configure ALB and Auto Scaling | Complete load balancing and scaling |
| Week 6 | Configure CloudWatch | Complete monitoring |
| Week 7 | Test failover and Auto Scaling | Verify fault tolerance |
| Week 8 | Evaluate, optimize, and finalize the report | Complete the workshop and report |

*Important milestones*

Milestone 1: The Python application runs successfully on EC2.

Milestone 2: ALB distributes requests to multiple EC2 instances.

Milestone 3: Auto Scaling is working.

Milestone 4: RDS Multi-AZ is working.

Milestone 5: CloudWatch monitoring is complete.

Milestone 6: EC2 failure testing is successful.

Milestone 7: The report is complete.

## 6. Budget Estimate

*Infrastructure cost*
- Amazon EC2: $1.50/month (2 small instances)
- Application Load Balancer: $1.50/month (1 ALB)
- Amazon RDS: $2.00/month (small MySQL configuration)
- Amazon EBS: $0.50/month (storage)
- Amazon ECR: $0.10/month (Docker image storage)
- Amazon CloudWatch: $0.20/month (monitoring)
- Data transfer: $0.20/month (low traffic)

Total: approximately $6.00/month, $48.00 for 8 months.

## 7. Risk Assessment

| Risk | Level | Solution |
|---|---|---|
| EC2 failure | High | Use multiple EC2 instances and Auto Scaling |
| One AZ fails | High | Distribute EC2 instances across multiple AZs |
| ALB does not receive requests | Medium | Check Listener, Security Group, and Target Group |
| EC2 is in an Unhealthy state | High | Configure health checks correctly |
| Auto Scaling does not create EC2 instances | High | Check Launch Template, IAM Role, and Subnet |
| Database failure | High | Use RDS Multi-AZ |
| CPU spike | Medium | Configure Auto Scaling policies |
| Incorrect Security Group configuration | High | Open only the required ports |
| Docker container does not run | Medium | Check Docker Image, ECR, and User Data |
| Incorrect network configuration | Medium | Check Route Tables, Subnets, and Internet Gateway |

> In addition, during implementation, it is necessary to regularly check AWS Billing to avoid unexpected costs.

## 8. Expected Results

Expected outcomes:
- The web system remains operational even when an instance or an AZ fails.
- Traffic is evenly distributed through the ALB, and ASG automatically adjusts capacity.
- Data is securely stored on RDS and S3.
- CloudWatch monitoring provides timely alerts.
- A failover testing scenario and evaluation report are prepared to assess the effectiveness of the solution.
