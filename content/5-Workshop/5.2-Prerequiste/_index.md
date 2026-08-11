---
title : "Prerequiste"
date : 2024-01-01 
weight : 2 
chapter : false
pre : " <b> 5.2. </b> "
---

Before starting the implementation, the required AWS environment and application resources must be prepared. These prerequisites provide the foundation for deploying the Python web application and implementing the High Availability architecture.

#### 5.2.1. AWS Account and Region

An active **AWS account** is required to create and manage the AWS resources used throughout this workshop.

The AWS Region is selected before creating the resources. For this workshop, the selected Region is:

**AWS Region:** `ap-southeast-1`  
**Region:** Asia Pacific (Singapore)

The selected Region provides multiple **Availability Zones (AZs)**, which will be used later to distribute application instances and improve system availability.

**Figure 5.1. Available Availability Zones**
![Available Availability Zones](/images/5-Workshop/5.2-Prerequisite/availability-zones.png) 

#### 5.2.2. EC2 Key Pair

An **EC2 Key Pair** is prepared for secure access to the EC2 instances that will be created during the workshop.

The key pair is created from:

**EC2 → Network & Security → Key Pairs → Create key pair**

The private key is stored securely and will be used when connecting to the EC2 instance.

**Figure 5.2. EC2 Key Pair**

![EC2 Key Pair](/images/5-Workshop/5.2-Prerequisite/ec2-key-pair.png)

#### 5.2.3. Python Web Application

A Python-based web application is required for the workshop. The application will be deployed on Amazon EC2 and will later be used to verify the operation of the Application Load Balancer and Auto Scaling.

To make the Load Balancer behavior easier to verify, the application will display information identifying the EC2 instance that handles each request, such as the **Hostname** and **Instance ID**.

The application source code is prepared before the deployment phase.

**Figure 5.3. Python Web Application Source Code**

![Source Code của ứng dụng Web Python](/images/5-Workshop/5.2-Prerequisite/python-project.png)

#### 5.2.4. Prerequisite Verification

Before proceeding to the implementation phase, the following prerequisites are verified:

| Prerequisite | Status |
|---|---|
| AWS account | Ready |
| AWS Region | `ap-southeast-1` |
| Multiple Availability Zones | Available |
| EC2 Key Pair | Created |
| Python Web Application | Prepared |

After completing these prerequisites, the environment is ready for the configuration of the AWS network infrastructure.
