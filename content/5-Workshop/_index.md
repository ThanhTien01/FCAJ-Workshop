---
title: "Workshop"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# HIGH AVAILABILITY ON AWS

#### Overview

In the cloud environment, ensuring that a system remains stable and continuously available is one of the most important requirements for online applications and services. When a server or one component of the system fails, if there is no failover mechanism, the application may be disrupted and directly impact users.

The topic "High Availability on AWS" focuses on designing and deploying a web application system that can maintain operation, tolerate faults, and automatically recover when incidents occur. The system is deployed across multiple Availability Zones to reduce single points of failure and increase continuous availability.

In this workshop, the application is deployed on Amazon EC2 and uses an Application Load Balancer (ALB) to distribute traffic to servers. Auto Scaling is used to automatically adjust the number of servers based on demand, while also replacing unhealthy servers. For data storage, the system can use Amazon RDS Multi-AZ to increase database redundancy.

In addition, Amazon CloudWatch is used to monitor the system’s status and performance, helping detect issues and generate alerts when necessary.

Through this topic, the participant has the opportunity to learn and practice the key principles of building a high availability system on AWS, from architecture design, application deployment, traffic distribution, and automatic scaling to failover testing. The topic illustrates how AWS can be used to build systems with high stability, scalability, and resiliency.

#### Contents

1. [Workshop Overview](5.1-Workshop-overview/)
2. [Preparation](5.2-Prerequiste/)
3. [Configure the AWS Network](5.3-Configure-the-AWS-Network/)
4. [Deploy the Python Web Application](5.4-Deloy-Python)
5. [Configure Amazon RDS and Amazon S3](5.5-Configure-RDS&S3)
6. [Configure Target Group and Health Check](5.6-TargetGroup&HealthCheck)
7. [Configure Application Load Balancer](5.7-Auto-Load-Balancer)
8. [Configure Launch Template](5.8-Launch-Template)
9. [Configure Auto Scaling](5.9-Auto-Scaling)
10. [Configure CloudWatch and Test](5.10-CloudWatch)
11. [Cleanup Resources](5.11-Cleanup)
12. [Results and Conclusion](5.12-Result-Conclusion)
