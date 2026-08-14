---
title: "Configure CloudWatch and Test Failover"
date: 2024-01-01
weight: 10
chapter: false
pre: " <b> 5.10. </b> "
---

After completing the Auto Scaling Group configuration, the next step is to use Amazon CloudWatch to monitor system performance and perform Failover testing. CloudWatch helps monitor metrics such as EC2 CPU utilization, while the Failover process verifies the system's ability to automatically recover when a server fails.

### 5.10.1. Configure Amazon CloudWatch

#### Step 1: Access CloudWatch
1. Open AWS Console.
2. Search for and select CloudWatch.
3. Select All metrics.
4. Select EC2 to view EC2 metrics.

#### Step 2: Monitor EC2 CPU

In CloudWatch → Metrics → All metrics → EC2 → Per-Instance Metrics, select the EC2 instances belonging to the Auto Scaling Group.

Monitor the metric:
```
CPU Utilization
```

> This metric shows the CPU usage of the EC2 instance over time.

![alt text](/images/5-Workshop/5.10/5.10.1.png)
**Figure 5.10.1. Monitor the CPUUtilization metric of EC2**

#### Step 3: Create a CloudWatch Alarm

To monitor when CPU increases:

1. Select Alarms → Create alarm.
2. Select the CPUUtilization metric.
3. Choose the EC2 instance to monitor.
4. Configure the condition:
```
Metric: CPUUtilization
Threshold type: Static
Condition: Greater than
Threshold: 70%
```

5. Set the alarm name:
```
workshop-high-cpu-alarm
```

6. Click Create alarm.

> When CPU exceeds 70%, the CloudWatch Alarm will transition to an In alarm state.

![alt text](/images/5-Workshop/5.10/5.10.2.png)
**Figure 5.10.2. Configure CloudWatch Alarm**

### 5.10.2. Test Failover

Failover testing is performed to verify the system's ability to continue operating when an EC2 instance fails.

In this workshop, the test is performed by terminating an active EC2 instance in the Auto Scaling Group.

#### Step 1: Check Initial Status

Before performing Failover, verify:

EC2 → Auto Scaling Groups → workshop-asg

Ensure the system has:
```
Desired capacity: 2
Minimum capacity: 2
Maximum capacity: 4
```

Check the Target Group:
```
EC2-01 → Healthy
EC2-02 → Healthy
```

![alt text](/images/5-Workshop/5.10/5.10.3.png)
**Figure 5.10.3. System status before Failover testing**

#### Step 2: Terminate an EC2 Instance
1. Go to EC2 → Instances.
2. Select an EC2 instance in the Auto Scaling Group.
3. Select Instance state → Terminate instance.
4. Confirm the termination.

After the EC2 is terminated, the number of instances in the system will temporarily decrease.

![alt text](/images/5-Workshop/5.10/5.10.5.png)
**Figure 5.10.5. Terminate EC2 to test Failover**

#### Step 3: Check Auto Scaling

Navigate to:
```
EC2 → Auto Scaling Groups → workshop-asg → Activity
```

Auto Scaling will detect that the number of EC2 instances is below the Desired capacity and automatically launch a new EC2 instance.

The process can be described as:
```
EC2-01 fails
      ↓
Auto Scaling detects
      ↓
Launch new EC2
      ↓
New EC2 added to Target Group
      ↓
Health Check
      ↓
Healthy
```

![alt text](/images/5-Workshop/5.10/5.10.6.png)
**Figure 5.10.6. Auto Scaling automatically launches replacement EC2**

#### Step 4: Check Target Group

Navigate to:
```
EC2 → Target Groups → workshop-tg → Targets
```

Check the status of the EC2 instances.

After the new EC2 is operational, the Target Group will display:
```
EC2-02 → Healthy
EC2-03 → Healthy
```

This indicates that the new EC2 has passed the Health Check and is ready to receive traffic from the ALB.

#### Step 5: Verify Application

Access the DNS Name of the Application Load Balancer:
```
http://fca-web-alb-1842986293.ap-southeast-1.elb.amazonaws.com
```

The application remains accessible after an EC2 is terminated, confirming that the Failover process has worked successfully.

### 5.10.3. Evaluate Test Results

The test results can be summarized as follows:

| Test Item | Result |
| --- | --- |
| CloudWatch monitors CPU | Success |
| EC2 failure scenario | Tested |
| Auto Scaling detects missing EC2 | Success |
| New EC2 created | Success |
| Target Group Health Check | Healthy |
| ALB continues distributing requests | Success |
| Application continues operating | Success |

Through this testing process, the system maintained its ability to serve users when an EC2 instance was terminated. Auto Scaling automatically created a replacement EC2, and the Target Group performed Health Checks before adding the new EC2 instance into service.
