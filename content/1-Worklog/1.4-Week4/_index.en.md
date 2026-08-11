---
title: "Week 4 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---


### Week 4 Objectives:

* Deploy the core system components to the AWS environment.
* Set up EC2 to run the backend application and deploy the main service.
* Create and configure Amazon RDS to store critical application data.
* Use Amazon S3 to store static data and necessary files.
* Verify connectivity between components and ensure the system operates stably.

### Tasks completed this week:

| Day | Work | Start Date | End Date | Source |
| --- | --- | --- | --- | --- |
| 2 | - Determine the appropriate EC2 configuration for the Python application <br> - Choose the required AMI, instance type, and storage | 13/07/2026 | 13/07/2026 | <https://aws.amazon.com/ec2/> |
| 3 | - Create the EC2 instance on AWS <br> - Configure the security group, key pair, and SSH access <br> - Connect to the instance from the local machine | 14/07/2026 | 14/07/2026 | <https://aws.amazon.com/ec2/> |
| 4 | - Install the runtime environment for the application on EC2 <br> - Install Python, dependencies, and configure the server | 15/07/2026 | 15/07/2026 | <https://aws.amazon.com/ec2/> |
| 5 | - Create the Amazon RDS instance <br> - Set up the database, parameter group, and connection from the EC2 application | 16/07/2026 | 16/07/2026 | <https://aws.amazon.com/rds/> |
| 6 | - Create the S3 bucket and configure access permissions <br> - Check the full data flow from EC2 to RDS and S3 <br> - Record issues and optimize the configuration | 17/07/2026 | 17/07/2026 | <https://aws.amazon.com/s3/> |

### Achievements this week:

* Successfully deployed an EC2 instance on AWS as the foundation for running the application.
* Successfully configured the key pair, security group, and SSH access to manage the instance from the local machine.
* Installed the Python environment on EC2 and ensured the demo application could run on the cloud server.
* Created and configured Amazon RDS to store system data and verified connectivity from the EC2 application.
* Used Amazon S3 to store static data, uploaded files, and supporting resources for the system.
* Gained a clear understanding of how the main AWS components interact: EC2 - RDS - S3.
* Verified the data flow and confirmed that the basic connection, security, and access settings were working correctly.
* Identified and fixed several issues during deployment, including incorrect port configuration, missing IAM permissions, and database connection errors.

### Lessons learned:

* Deploying an application to AWS is not only about creating an instance; it also requires proper network configuration, security groups, and access permissions to avoid connection issues.
* EC2 is a critical component for running the application, but to ensure stable operation, the system also needs a database such as RDS and static storage such as S3.
* RDS helps reduce the application’s operational burden in managing data and ensures the durability of critical information.
* S3 is an effective solution for storing files, images, backups, or data that requires fast retrieval.
* During deployment, verifying each step carefully—from SSH, security groups, and database connection strings to permissions—helps minimize risk and debugging time.

### Overall assessment:

Week 4 marked the transition from local development to cloud deployment. By deploying EC2, RDS, and S3, I gained a clearer understanding of how the components in an AWS system work together to create a real application that can run stably. This is an important foundation for the following weeks, when the system will be expanded and optimized with advanced services such as Load Balancer, Auto Scaling, and Monitoring.
