---
title: "Week 5 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.5. </b> "
---


### Week 5 Objectives:

* Understand and deploy the Application Load Balancer to distribute traffic across the system.
* Configure the Auto Scaling Group to improve application availability and scalability.
* Evaluate system stability when instance count and traffic volume change.
* Understand the process of configuring target groups, health checks, and scale-out/scale-in policies.

### Tasks completed this week:

| Day | Work | Start Date | End Date | Source |
| --- | --- | --- | --- | --- |
| 2 | - Learn the AWS Load Balancer architecture <br> - Compare ALB with other load balancing models | 20/07/2026 | 20/07/2026 | <https://aws.amazon.com/elasticloadbalancing/> |
| 3 | - Create a target group for EC2 instances <br> - Configure health checks and healthy/unhealthy status | 21/07/2026 | 21/07/2026 | <https://aws.amazon.com/elasticloadbalancing/> |
| 4 | - Deploy the Application Load Balancer <br> - Configure listeners, ports, protocols, and routing | 22/07/2026 | 22/07/2026 | <https://aws.amazon.com/elasticloadbalancing/> |
| 5 | - Create the Auto Scaling Group <br> - Configure the launch template and min/max/desired capacity | 23/07/2026 | 23/07/2026 | <https://aws.amazon.com/autoscaling/> |
| 6 | - Configure scale-out / scale-in policies based on CPU <br> - Test instance scaling up and down and evaluate the results | 24/07/2026 | 24/07/2026 | <https://aws.amazon.com/autoscaling/> |

### Achievements this week:

* Clearly understood the role of the Application Load Balancer in distributing traffic and improving system availability.
* Successfully configured target groups and health checks so ALB could determine the health status of EC2 instances.
* Deployed ALB on AWS and configured listeners to forward requests to the application.
* Gained a solid understanding of how the Auto Scaling Group operates by adjusting instance capacity and automatically replacing unhealthy instances.
* Created a launch template to standardize EC2 configuration when Auto Scaling expands or recreates instances.
* Successfully configured scale-out and scale-in policies based on CPU usage and other system metrics.
* Tested the process of increasing the number of instances under high load and reducing them when demand decreased.
* Observed the clear benefits of Load Balancer and Auto Scaling in improving stability, increasing traffic handling capacity, and reducing downtime risk.

### Lessons learned:

* Load Balancers help distribute traffic evenly, prevent a single instance from becoming overloaded, and improve application availability.
* Health checks are essential so ALB can identify which instances are healthy and which should be removed from the traffic distribution pool.
* Auto Scaling is an effective solution for dynamically expanding resources based on real demand, helping optimize costs and increase flexibility.
* When configuring Auto Scaling, it is necessary to define min, max, and desired capacity carefully to avoid over-scaling or insufficient capacity during peak load periods.
* Testing scale-out/scale-in policies helps evaluate how quickly the system responds under changing traffic conditions.

### Overall assessment:

Week 5 was a crucial stage in the system deployment process, as I moved from running the application on a single EC2 instance to a higher-availability model. With the configuration of Load Balancer and Auto Scaling, the system was able to distribute traffic and automatically adjust based on workload. This was a major upgrade that brought the system closer to the High Availability architecture and laid the foundation for the following weeks on monitoring, failover, and performance optimization.
