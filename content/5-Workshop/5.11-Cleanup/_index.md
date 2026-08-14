---
title : "Cleanup Resources"
date : 2024-01-01
weight : 11
chapter : false
pre : " <b> 5.11. </b> "
---
After completing the Workshop and testing High Availability capabilities, you need to clean up the AWS resources that were created. This helps avoid unnecessary costs and ensures that your AWS account does not have unused resources running after the Workshop ends.

### 5.11.1. Delete Auto Scaling Group

Navigate to:

AWS Console → EC2 → Auto Scaling Groups

1. Select workshop-asg.
2. Select Delete.
3. Confirm deletion of the Auto Scaling Group.
4. Verify that the EC2 instances managed by Auto Scaling have been terminated.
![alt text](/images/5-Workshop/5.11/delete-asg.png)
**Figure 5.11.1. Delete Auto Scaling Group**

### 5.11.2. Delete Application Load Balancer

Navigate to:

EC2 → Load Balancers

1. Select workshop-alb.
2. Select Actions → Delete load balancer.
3. Confirm Delete.

>After deletion, check the Load Balancer list to ensure that workshop-alb no longer exists.

![alt text](/images/5-Workshop/5.11/delete-alb.png)
**Figure 5.11.2. Delete Application Load Balancer**

### 5.11.3. Delete Target Group

Navigate to:

EC2 → Target Groups

1. Select workshop-tg.
2. Select Actions → Delete.
3. Confirm deletion of the Target Group.

![alt text](/images/5-Workshop/5.11/delete-target.png)
**Figure 5.11.3. Delete Target Group**

### 5.11.4. Delete Launch Template

Navigate to:

EC2 → Launch Templates

1. Select workshop-launch-template.
2. Select Actions → Delete template.
3. Confirm deletion.

>Although Launch Template does not incur direct costs, it is good practice to delete it to avoid leaving unnecessary configurations in your account.

![alt text](/images/5-Workshop/5.11/delete-launch.png)
**Figure 5.11.4. Delete Launch Template**

### 5.11.5. Delete Amazon RDS

If the Workshop created an RDS Database and it is no longer needed:

1. Navigate to AWS Console → RDS.
2. Select Databases.
3. Select the Database workshop-db.
4. Select Actions → Delete.
5. Disable the option to create a final snapshot if the Database was only used for the Workshop and you do not need to retain the data.
6. Confirm deletion of the Database.

![alt text](/images/5-Workshop/5.11/delete-rds.png)
**Figure 5.11.5. Delete Amazon RDS**

>Be careful before deleting as this action may result in data loss from the Database.

### 5.11.6. Delete data on Amazon S3

If you do not need the Bucket after the Workshop:

1. Navigate to AWS Console → S3.
2. Select the Bucket that was created.
3. Select Empty to delete all data.
4. Confirm deletion of the data.
5. Select Bucket → Delete.
6. Enter the Bucket name to confirm.

![alt text](/images/5-Workshop/5.11/delete-s3.png)
**Figure 5.11.6. Delete Amazon S3 Bucket**

### 5.11.7. Delete network resources

After dependent resources have been deleted, proceed to delete the network components:

- Security Groups that are no longer in use.
- Route Tables that are no longer in use.
- Internet Gateway.
- Subnets.
- VPC.

Perform this at:
```
AWS Console → VPC
```

>You must delete dependent resources first. For example, you cannot delete a VPC while EC2 instances, Load Balancers, or other network resources are still using it.

### 5.11.8. Verification and Completion

After cleanup, verify the following services:
| Service                   | Status                   |
| --- | --- |
| EC2                       | Terminated             |
| Auto Scaling Group        | Deleted                   |
| Application Load Balancer | Deleted                   |
| Target Group              | Deleted                   |
| Launch Template           | Deleted                   |
| Amazon RDS                | Deleted                   |
| Amazon S3                 | Deleted                   |
| VPC and Network           | Deleted if not in use |
| CloudWatch Alarm          | Deleted                   |

>Finally, you can access AWS Billing and Cost Management to verify that no remaining resources are incurring costs.
