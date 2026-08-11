---
title : "Create a VPC"
date : 2024-01-01 
weight : 1
chapter : false
pre : " <b> 5.3.1 </b> "
---

The first step in preparing the AWS network infrastructure is to create an **Amazon Virtual Private Cloud (VPC)**.

The VPC provides an isolated virtual network for the AWS resources used in the workshop. The application resources will be deployed within this VPC in the following steps.

Navigate to:

**AWS Management Console → VPC → Your VPCs → Create VPC**

Under **Resources to create**, select:

**VPC only**

The VPC is configured with the following parameters:

| Configuration | Value |
|---|---|
| **Name tag** | `fca-workshop-vpc` |
| **IPv4 CIDR block** | `10.0.0.0/16` |
| **IPv6 CIDR block** | No IPv6 CIDR block |
| **Tenancy** | Default |

After completing the configuration, select **Create VPC**.

The created VPC is then verified under **Your VPCs**. The VPC should have an **Available** status and the configured IPv4 CIDR block.

**Figure 5.3. VPC Configuration**
![VPC Configuration](/images/5-Workshop/5.3-configure-the-aWS-network/vpc-created.png)