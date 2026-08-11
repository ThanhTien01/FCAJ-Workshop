---
title : "Introduction"
date : 2024-01-01 
weight : 1 
chapter : false
pre : " <b> 5.1. </b> "
---

Cloud computing has become an important foundation for modern information technology systems. As web applications serve an increasing number of users, ensuring system availability, reliability, and the ability to respond to changing workloads has become an important requirement. A web application deployed on a single server may become unavailable when the server experiences a hardware failure, network problem, or unexpected increase in traffic. This creates a **Single Point of Failure (SPOF)** and can lead to service interruption.

![Multi-AZ High Availability Architecture](/images/5-Workshop/5.1-Workshop-overview/multi-az-architecture.png)

**High Availability (HA)** is an approach used to minimize service downtime by distributing application resources across multiple independent infrastructure components. On AWS, High Availability can be achieved by combining multiple **Availability Zones (AZs)** with services such as **Amazon EC2, Amazon RDS, Application Load Balancer, Auto Scaling, Amazon S3, and Amazon CloudWatch**. These services provide different capabilities for computing, database management, traffic distribution, automatic resource scaling, storage, monitoring, and system recovery.

In this workshop, a **Python-based web application** is deployed on AWS and designed to operate across multiple Availability Zones. An **Application Load Balancer (ALB)** is used to distribute incoming requests to healthy application servers, while an **Auto Scaling Group (ASG)** automatically adjusts the number of EC2 instances according to the system workload. Amazon RDS is used to provide a managed database service, while Amazon S3 provides cloud-based object storage. Amazon CloudWatch is also configured to monitor system performance and operational activities.

![Single Point of Failure Architecture](/images/5-Workshop/5.1-Workshop-overview/spof-architecture.png)

The workshop focuses not only on deploying the application but also on **testing the availability and fault tolerance of the system**. Failover scenarios are performed by simulating the failure of an application instance and observing how the Load Balancer and Auto Scaling Group respond. The results are then evaluated to determine whether the system can maintain service availability and automatically recover from individual resource failures.

The overall implementation follows the planned eight-week internship timeline, including studying High Availability concepts, designing the Multi-AZ architecture, deploying the application, configuring AWS services, implementing Load Balancing and Auto Scaling, setting up monitoring and logging, performing failover testing, and evaluating the final system.