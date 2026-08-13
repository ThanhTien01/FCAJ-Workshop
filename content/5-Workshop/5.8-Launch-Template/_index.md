---
title: "Launch Template Configuration"
date: 2024-01-01
weight: 8
chapter: false
pre: " <b> 5.8. </b> "
---

After completing the Application Load Balancer configuration, the next step is to create a Launch Template. A Launch Template stores the required configuration information to launch new EC2 instances, such as the AMI, instance type, key pair, and security group.

The Launch Template will be used by the Auto Scaling Group to automatically create EC2 instances with the same configuration. This is an important component that helps the system scale and recover automatically when an EC2 instance fails.

### 5.8.1. Create a Launch Template

#### Step 1: Access Launch Templates
1. Go to AWS Console → EC2.
2. In the left menu, select Launch Templates.
3. Choose Create launch template.

![alt text](/images/5-Workshop/5.8/5.8.1.png)
**Figure 5.8.1. Launch Template creation interface**

#### Step 2: Configure Launch Template Information

In the Launch template name and description section, enter:
```
Launch template name: workshop-launch-template
Description: Launch Template for High Availability Workshop
```

### 5.8.2. Select the Amazon Machine Image

In the Application and OS Images (Amazon Machine Image) section:

1. Select Quick Start.
2. Choose Ubuntu.
3. Select the Ubuntu version currently used for the EC2 instance created earlier.
```
AMI: Ubuntu Server 24.04 LTS
Architecture: 64-bit (x86)
```

It is recommended to use the same AMI as the EC2 instance that was previously deployed for the application to ensure the EC2 instances created by Auto Scaling have a similar environment.

![alt text](/images/5-Workshop/5.8/5.8.2.png)
**Figure 5.8.2. Selecting the AMI for the Launch Template**

#### 5.8.3. Configure Instance Type and Key Pair

In the Instance type section, choose a small instance type suitable for the workshop:
```
Instance type: t3.micro
```

In the Key pair section, select the key pair created earlier:
```
Key pair: fca-workshop-key
```

The key pair is used to connect to and administer the EC2 instance when needed.

![alt text](/images/5-Workshop/5.8/5.8.3.png)
**Figure 5.8.3. Configuring the Instance Type and Key Pair**

### 5.8.4. Configure the Security Group

In the Network settings section, select the security group for the EC2 instance.

```
Security Group: workshop-sg
```

This security group must allow the necessary connections for the system.

In the complete architecture, it is recommended to configure:
```
ALB Security Group
        │
        │ HTTP : 5000
        ▼
EC2 Security Group
```

Instead of allowing direct public access to the application port.

![alt text](/images/5-Workshop/5.8/5.8.4.png)
**Figure 5.8.4. Security Group configuration**

### 5.8.5. Configure User Data

To ensure the EC2 instances created automatically can run the Python application, User Data can be used to install the environment and start the application when the EC2 instance is created.

In Advanced details → User data, enter the script appropriate for the application.

![alt text](/images/5-Workshop/5.8/5.8.5.png)
**Figure 5.8.5. User Data configuration**

### 5.8.6. Create the Launch Template

After completing the configurations:

1. Recheck the AMI.
2. Recheck the instance type.
3. Recheck the key pair.
4. Recheck the security group.
5. Recheck the user data.
6. Select Create launch template.

Once created successfully, the Launch Template will appear in the list:
```
workshop-launch-template
Version: 1
```

![alt text](/images/5-Workshop/5.8/5.8.6.png)
**Figure 5.8.6. Launch Template created successfully**
