---
title: "AWS Network Configuration"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 5.3. </b> "
---

### Step 1: Create VPC

The first step in building the AWS network infrastructure is to create an **Amazon Virtual Private Cloud (VPC)**.

The VPC provides an isolated virtual network for the AWS resources used in the workshop. The application resources will be deployed inside this VPC in later steps.

Navigate to:

**AWS Management Console → VPC → Your VPCs → Create VPC**

In the **Resources to create** section, choose:

**VPC only**

Configure the VPC as follows:

| Configuration | Value |
|---|---|
| **Name tag** | `fca-workshop-vpc` |
| **IPv4 CIDR block** | `10.0.0.0/16` |
| **IPv6 CIDR block** | No IPv6 CIDR block |
| **Tenancy** | Default |

After finishing the configuration, click **Create VPC**.

Verify the VPC you created under **Your VPCs**. The VPC should have status **Available** and show the correct IPv4 CIDR block.

**Figure 5.3. VPC Configuration**
![VPC Configuration](/images/5-workshop/5.3-Configure-the-AWS-Network/vpc-created.png)

### Step 2: Create Subnets

After creating the VPC, two subnets are created in different **Availability Zones**.

Distributing subnets across multiple Availability Zones creates a network foundation for deploying application resources with better availability and fault tolerance.

The subnets created inside `fca-workshop-vpc` are:

| Subnet | Availability Zone | IPv4 CIDR |
|---|---|---|
| `fca-public-subnet-a` | `ap-southeast-1a` | `10.0.1.0/24` |
| `fca-public-subnet-b` | `ap-southeast-1b` | `10.0.2.0/24` |

The first subnet is created in `ap-southeast-1a` with CIDR `10.0.1.0/24`.

The second subnet is created in `ap-southeast-1b` with CIDR `10.0.2.0/24`.

After creating both subnets, review the configuration under **VPC → Subnets**.

**Figure 5.4. Subnets distributed across two Availability Zones**
![Subnets distributed across two Availability Zones](/images/5-Workshop/5.3-Configure-the-AWS-Network/subnets-created.png)

### Step 3: Create Internet Gateway and Route Table

After creating the VPC and subnets, the next step is to configure the Internet Gateway (IGW) and Route Table so that resources in the Public Subnet can connect to the Internet. This step is necessary for EC2 instances to access the Internet and for users to access the web application.

#### Create Internet Gateway

1. Open the AWS Console and go to VPC.
2. Select Internet gateways from the left menu.
3. Click Create internet gateway.
4. Enter the name:
```workshop-igw```
5. Click Create internet gateway.

![InternetGateway](/images/5-Workshop/5.3/internetgateway.png)
**Figure 5.5. Internet Gateway created**

#### Attach Internet Gateway to the VPC

1. Select the Internet Gateway you created.
2. Choose Actions → Attach to a VPC.
3. In Available VPCs, choose the VPC created in the previous step.
4. Click Attach internet gateway.

![Attach internet gateway to vpc](/images/5-Workshop/5.3/igwtovpc.png)
**Figure 5.6. Internet Gateway attached to the VPC**

#### Create Route Table

1. In the VPC Console, select Route tables.
2. Click Create route table.
3. Enter:
- Name: `workshop-public-rt`
- VPC: select the workshop VPC.
4. Click Create route table.

![route-table](/images/5-Workshop/5.3/route-table.png)
**Figure 5.7. Route Table created**

#### Add Internet Route

Select `workshop-public-rt` → Routes tab → Edit routes → Add route.

Configure:
```
Destination: 0.0.0.0/0
Target: Internet Gateway
        workshop-igw
```

Then click Save changes.

Route **0.0.0.0/0** allows traffic from the Public Subnet to be routed to the Internet through the Internet Gateway.

![add-internet-route](/images/5-Workshop/5.3/add-internet-route.png)
**Figure 5.8. Internet route added**

#### Associate Route Table with Public Subnets

1. Select the Subnet associations tab.
2. Click Edit subnet associations.
3. Select the Public Subnets created earlier.
4. Click Save associations.

![Associate rt with public subnet](/images/5-Workshop/5.3/rt-to-subnet.png)

**Figure 5.9. Route Table associated with Public Subnets**

### Verification

After completion, verify that:

- The Internet Gateway is in the Attached state.
- The Route Table contains the route 0.0.0.0/0.
- The Route Table is associated with the Public Subnets.
- The Public Subnets are using the correct Route Table.

*Result:* The Public Subnets now have Internet connectivity through the Internet Gateway, providing the foundation for deploying EC2 and the Application Load Balancer in subsequent steps.
