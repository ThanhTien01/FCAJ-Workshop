---
title: "Configure Auto Scaling"
date: 2024-01-01
weight: 9
chapter: false
pre: " <b> 5.9. </b> "
---

After completing the Launch Template and Application Load Balancer configuration, the next step is to configure the Auto Scaling Group (ASG). Auto Scaling enables the system to automatically adjust the number of EC2 instances based on demand, while also replacing failed servers with new instances.

In this workshop, Auto Scaling is configured with an initial setup of 2 EC2 instances distributed across 2 Availability Zones, with the ability to scale up to a maximum of 4 EC2 instances.

### 5.9.1. Create an Auto Scaling Group

#### Step 1: Access Auto Scaling Groups
1. Access AWS Console → EC2.
2. In the left menu, select Auto Scaling Groups.
3. Select Create Auto Scaling group.

![alt text](/images/5-Workshop/5.9/create-asg.png)
**Figure 5.9.1. Auto Scaling Group creation interface**

#### Step 2: Name the Auto Scaling Group

In the Choose launch template or configuration section:
```
Auto Scaling group name:
workshop-asg
```

For the Launch template, select:
```
Launch Template:
workshop-launch-template
Version:
Latest
```

Then click Next.

![alt text](/images/5-Workshop/5.9/launch-template.png)
**Figure 5.9.2. Launch Template selection**

### 5.9.2. Configure Network

In the Network section:

1. Select the VPC you created.
2. Under Availability Zones and subnets, select subnets from different Availability Zones.

Selecting multiple Availability Zones distributes EC2 instances across independent regions, improving system fault tolerance.

![alt text](/images/5-Workshop/5.9/network.png)
**Figure 5.9.3. Configure Availability Zones and Subnets**

### 5.9.3. Attach Auto Scaling to the Target Group

In the Configure advanced options section:

1. Select:
```
Load balancing: Attach to an existing load balancer
```

2. Choose the Target Group you created:
```
fca-web-target-group
```

3. Enable:
```
Turn on Elastic Load Balancing health checks
```

4. Configure:
```
Health check grace period: 300 seconds
```

Health Checks help Auto Scaling determine whether EC2 instances are operating normally.

> If an EC2 instance fails and remains in an unhealthy state, Auto Scaling can remove that instance and create a new one as a replacement.

### 5.9.4. Configure Capacity

In the Group size section, configure:
```
Desired capacity: 2
Minimum capacity: 2
Maximum capacity: 4
```

Meaning:
| Parameter | Value | Description |
| --- | --- | --- |
| Desired | 2 | Initial desired number of EC2 instances |
| Minimum | 2 | Do not fall below 2 EC2 instances |
| Maximum | 4 | Do not exceed 4 EC2 instances |

![alt text](/images/5-Workshop/5.9/group-size.png)
**Figure 5.9.4. Configure Desired, Minimum, and Maximum Capacity**

### 5.9.5. Set Up Scale Out / Scale In Policies

In the Configure group size and scaling section, select a scaling policy:
```
Scaling type:
Target tracking scaling policy
```

Choose the metric:
```
Average CPU utilization
```

Set the target value:
```
Target value: 50%
```

This means Auto Scaling will attempt to maintain the average CPU utilization of the EC2 instances at approximately 50%.

```
CPU > 50%
     ↓
Scale Out
     ↓
2 EC2 → 3 EC2 → 4 EC2
```

When load decreases:
```
CPU < 50%
     ↓
Scale In
     ↓
4 EC2 → 3 EC2 → 2 EC2
```

![alt text](/images/5-Workshop/5.9/scaling.png)
**Figure 5.9.5. Configure Target Tracking Scaling Policy**

> For this workshop, Target Tracking is used as a simple way to demonstrate the automatic Scale Out and Scale In mechanism.

### 5.9.6. Complete Auto Scaling Group Setup

After completing all configurations:

1. Verify the Launch Template.
2. Verify the VPC and Subnets.
3. Verify the Target Group.
4. Verify the Desired, Minimum, and Maximum Capacity values.
5. Verify the Scaling Policy.
6. Click Create Auto Scaling group.
