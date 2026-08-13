---
title: "Week 7 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.7. </b> "
---

### Week 7 Objectives:

* Evaluate the system’s fault-tolerance using real failover scenarios.
* Simulate an EC2 instance failure and assess the response of the Load Balancer, Auto Scaling, and the application.
* Confirm system availability after a component failure occurs.
* Collect data and assess the effectiveness of the High Availability architecture.

### Tasks completed this week:

| Day | Work | Start Date | End Date | Source |
| --- | --- | --- | --- | --- |
| 2 | - Plan the failover test and identify the failure scenarios to simulate | 03/08/2026 | 03/08/2026 | <https://aws.amazon.com/ec2/> |
| 3 | - Simulate an EC2 instance failure by stopping the instance or shutting down the virtual machine | 04/08/2026 | 04/08/2026 | <https://aws.amazon.com/ec2/> |
| 4 | - Monitor the state of the ALB, target group, and Auto Scaling Group during failover | 05/08/2026 | 05/08/2026 | <https://aws.amazon.com/elasticloadbalancing/> |
| 5 | - Check the application after the instance failure and confirm that the system continues serving users | 06/08/2026 | 06/08/2026 | <https://aws.amazon.com/autoscaling/> |
| 6 | - Consolidate the results, assess latency, recovery time, and solution effectiveness | 07/08/2026 | 07/08/2026 | <https://aws.amazon.com/cloudwatch/> |

### Achievements this week:

* Successfully conducted failover tests to evaluate the system’s fault tolerance.
* Simulated an EC2 instance failure and observed the system redirect traffic through the ALB to the remaining healthy instance.
* Confirmed that the Auto Scaling Group could automatically replace the failed instance or launch a new one when needed.
* Evaluated the system recovery time during scenarios where a node or service became unavailable.
* Verified the effectiveness of health checks in detecting unhealthy instances and removing them from the target group.
* Observed that the system remained operational in most failover scenarios tested.
* Collected data on latency, availability, and application stability before and after the failure event.

### Lessons learned:

* Failover testing is crucial to confirm that the system can truly handle faults, not just in theory but in practice.
* The Load Balancer and Auto Scaling play a central role in minimizing downtime when an instance fails.
* Health checks are an important mechanism for identifying inactive instances and preventing traffic from being routed to unhealthy nodes.
* A High Availability system does not need to avoid failures completely; it needs to minimize downtime and continue delivering service to users.
* The test results confirmed that a distributed and redundant architecture is essential for system availability.

### Overall assessment:

Week 7 was the stage where I evaluated the real effectiveness of the AWS solution I had deployed. Through simulated failures and failover testing, I clearly saw the contribution of ALB, Auto Scaling, and CloudWatch in improving system stability and availability. The test results showed not only that the system could recover after an error, but also helped me identify areas for improvement to continue optimizing the architecture in the future.
