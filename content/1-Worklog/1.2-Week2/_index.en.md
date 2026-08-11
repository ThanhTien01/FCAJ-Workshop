---
title: "Worklog Week 2"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.2. </b> "
---

### Week 2 Objectives:

* Design a high-availability architecture on AWS.
* Apply Multi-AZ and Load Balancer to reduce downtime and increase fault tolerance.
* Identify the AWS service components needed for the HA solution.

### Tasks planned for this week:
| Day | Task                                                                                                                                                                             | Start Date | End Date | Resources                                  |
| --- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------- | -------- | ------------------------------------------ |
| 2   | - Collect project requirements and HA system goals <br> - Determine the appropriate AWS architectural components                                                                | 29/06/2026 | 29/06/2026 |                                            |
| 3   | - Study Multi-AZ architecture for EC2 and RDS <br> - Learn how Elastic Load Balancer (ALB/NLB) works <br> - Define VPC and subnet networking models                                | 30/06/2026 | 30/06/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Design the system diagram: <br>&emsp; + EC2 across multiple Availability Zones <br>&emsp; + RDS Multi-AZ <br>&emsp; + S3 for static storage <br>&emsp; + ELB for traffic distribution and health checks | 01/07/2026 | 01/07/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Determine network and security configuration: <br>&emsp; + VPC, Public/Private subnets <br>&emsp; + Route Tables <br>&emsp; + Security Groups <br>&emsp; + NACL and IAM roles for EC2/RDS | 02/07/2026 | 02/07/2026 | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - Prepare the deployment test plan: <br>&emsp; + Check load balancer deployment priorities <br>&emsp; + Identify backup and recovery options <br>&emsp; + Compare costs            | 03/07/2026 | 03/07/2026 | <https://cloudjourney.awsstudygroup.com/> |


### Week 2 Results:

* Understood the high-availability architecture problem and the factors affecting system resilience.
* Designed a Multi-AZ model for EC2 with at least two Availability Zones to ensure fault tolerance in case one AZ fails.
* Planned the use of an Elastic Load Balancer to distribute traffic and perform instance health checks.
* Identified the use of RDS Multi-AZ to ensure the database has standby replicas and automatic failover.
* Clarified the VPC structure with public/private subnets, Security Group configuration, and Route Tables for HA architecture.
* Prepared the list of required AWS services for the architecture: EC2, ELB, RDS Multi-AZ, S3, CloudWatch, IAM.
* Defined failover test scenarios and basic monitoring strategies for the system.

### Lessons Learned:

* Building a high-availability architecture requires balancing performance, resilience, and cost.
* Multi-AZ reduces infrastructure failure risk, while Load Balancer ensures traffic distribution and unhealthy instance detection.
* Preparing the VPC, subnet, and security design is a fundamental step for stable HA operation.
* A clear deployment plan helps reduce mistakes when moving to AWS implementation.
