---
title: "Configure Target Group and Health Check"
date: 2024-01-01
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---

After deploying the Python application on EC2, the next step is to create a Target Group to manage the application-running EC2 instances. The Target Group is used by the Application Load Balancer (ALB) to distribute traffic to servers. Health Checks determine which EC2 instances are healthy and ready to receive requests.

### 1. Create a Target Group
#### Step 1: Open Target Groups
1. Open the AWS Console → EC2.
2. In the left menu, choose Target Groups.
3. Click Create target group.

![Target Group](/images/5-Workshop/5.6/target-group.png)
**Figure 5.6.1 — Target Group creation screen**

#### Step 2: Choose a target type
At "Choose a target type", select:
```
Target type: Instances
```
Then click Next.

#### Step 3: Configure the Target Group
Set the following parameters:
```
Target group name: workshop-tg
Protocol: HTTP
Port: 5000
IP address type: IPv4
VPC: fca-Workshop-vpc
Protocol version: HTTP1
```
Port 5000 is the port where the Python Flask application runs on EC2.

Example:
```
Application → 0.0.0.0:5000
Target Group → HTTP:5000
```
Then click Next.

### 2. Register EC2 instances to the Target Group
At the Register targets step:

1. Select the EC2 instances running the Python application.
2. Verify the port:
```
Port: 5000
```
3. Choose "Include as pending below." 
4. Verify the EC2 instances appear in the Review targets list.
5. Click Create target group.

![Register EC2 to Target Group](/images/5-Workshop/5.6/ec2-to-targetgroup.png)
**Figure 5.6.2 — Register EC2 instances to the Target Group**

After creation, go to:

EC2 → Target Groups → workshop-tg → Targets

You should see the EC2 instances registered to the Target Group.

### 3. Configure Health Check
Health Checks verify the application's health on EC2.

#### Step 1: Open Health Check settings
1. Choose Target Groups.
2. Select `workshop-tg`.
3. Open the Health checks tab.
4. Click Edit health check settings.

#### Step 2: Health Check configuration
Set:
```
Health check protocol: HTTP
Health check path: /
Health check port: Traffic port
Healthy threshold: 2
Unhealthy threshold: 2
Timeout: 5 seconds
Interval: 30 seconds
Success codes: 200
```
Notes:
- Health check path `/`: ALB sends requests to the application root.
- Success code `200`: an EC2 is considered healthy when the app returns HTTP 200.
- Healthy threshold `2`: requires 2 consecutive successful checks to mark healthy.
- Unhealthy threshold `2`: requires 2 consecutive failed checks to mark unhealthy.

Click Save changes.

### 4. Verify Target status
After configuring Health Checks:

1. Open EC2 → Target Groups.
2. Select `workshop-tg`.
3. Open the Targets tab.
4. Observe the Status column.

If the application is running correctly, the status should become:
```
healthy
```

![Healthy](/images/5-Workshop/5.6/5.6.3.png)
**Figure 5.6.3 — Target status is Healthy**

If a target is `unhealthy`, check:

- Whether the Python application is running.
- Whether the application port is set to `5000`.
- Whether the Security Group allows traffic to port `5000`.
- Whether the Health Check path `/` exists and returns a 200 status.

### 5. Result
After completion, the system will have a Target Group managing EC2 instances and Health Checks to determine application status.

```
                Target Group
                     │
              Health Check "/"
                     │
             ┌───────┴───────┐
             ▼               ▼
          EC2-01           EC2-02
           :5000             :5000
             │               │
          Healthy         Healthy
```

The Target Group acts as an intermediary between the Application Load Balancer and the EC2 instances. When multiple EC2 instances are deployed, the ALB sends requests only to Targets marked as `healthy`, improving application availability.
