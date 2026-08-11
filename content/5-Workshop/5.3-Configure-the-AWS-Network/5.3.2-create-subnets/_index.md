---
title : "Create Subnets"
date : 2024-01-01 
weight : 2
chapter : false
pre : " <b> 5.3.2 </b> "
---

After creating the VPC, two subnets are created in different **Availability Zones**.

Distributing the subnets across multiple Availability Zones provides the network foundation for deploying application resources with improved availability and fault tolerance.

The following subnets are created within `fca-workshop-vpc`:

| Subnet | Availability Zone | IPv4 CIDR |
|---|---|---|
| `fca-public-subnet-a` | `ap-southeast-1a` | `10.0.1.0/24` |
| `fca-public-subnet-b` | `ap-southeast-1b` | `10.0.2.0/24` |

The first subnet is created in `ap-southeast-1a` with the CIDR block `10.0.1.0/24`.

The second subnet is created in `ap-southeast-1b` with the CIDR block `10.0.2.0/24`.

After both subnets are created, the configuration is verified under **VPC → Subnets**.

**Figure 5.4. Subnets Distributed Across Two Availability Zones**
![Subnets Distributed Across Two Availability Zones](/images/5-workshop/5.3-Configure-the-AWS-Network/subnets-created.png)