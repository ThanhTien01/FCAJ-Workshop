---
title: "Week 6 Worklog"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.6. </b> "
---

### Week 6 Objectives:

* Set up a monitoring and logging system for the application on AWS.
* Understand how Amazon CloudWatch collects metrics and logs from EC2, ALB, and related services.
* Create alarms and alerts to respond quickly to incidents or abnormal traffic levels.
* Improve system administration through a centralized monitoring and logging model.

### Tasks completed this week:

| Day | Work | Start Date | End Date | Source |
| --- | --- | --- | --- | --- |
| 2 | - Learn the role of CloudWatch in monitoring AWS systems <br> - Study the different types of metrics, logs, and alarms | 27/07/2026 | 27/07/2026 | <https://aws.amazon.com/cloudwatch/> |
| 3 | - Configure CloudWatch on EC2 <br> - Enable basic metrics such as CPU, memory, disk, and network usage | 28/07/2026 | 28/07/2026 | <https://aws.amazon.com/cloudwatch/> |
| 4 | - Create a log group and send logs from the Python application to CloudWatch Logs <br> - Check the log format and structure | 29/07/2026 | 29/07/2026 | <https://aws.amazon.com/cloudwatch/> |
| 5 | - Create alert alarms for CPU, instance status, and system errors <br> - Test alerts when resource consumption increases | 30/07/2026 | 30/07/2026 | <https://aws.amazon.com/cloudwatch/> |
| 6 | - Consolidate monitoring data and evaluate monitoring effectiveness <br> - Record lessons learned and propose improvements for the system | 31/07/2026 | 31/07/2026 | <https://aws.amazon.com/cloudwatch/> |

### Achievements this week:

* Clearly understood the role of CloudWatch in monitoring, tracking, and alerting on AWS system issues.
* Successfully configured basic EC2 metrics such as CPU utilization, disk usage, and network traffic.
* Configured logs from the Python application and sent them to CloudWatch Logs for storage and real-time analysis.
* Learned how to manage log groups, log streams, and query log data when incidents occur.
* Created alert alarms for scenarios such as CPU overload, resource shortages, or system errors.
* Successfully tested the response capability of alarms when the system experienced high load or abnormal conditions.
* Gained the ability to analyze incident causes through metrics and logs, significantly reducing debugging time.
* Recognized the importance of monitoring and logging in maintaining system stability and availability.

### Lessons learned:

* Monitoring not only helps observe system status but also supports operational decisions during resource optimization and system management.
* CloudWatch provides an overview of the performance of EC2, ALB, and related services, helping detect potential failures early.
* Logs are a crucial data source for understanding incident causes, while metrics help evaluate trends in system load.
* Alarms are essential for reducing response time when issues arise, especially in production environments.
* A well-designed system must not only run stably but also include a clear monitoring mechanism so operators can proactively act when early warning signs appear.

### Overall assessment:

Week 6 focused on the operational side of the system, as the application had already been deployed and was running in the AWS environment. Setting up monitoring and logging with CloudWatch helped me understand how to track performance, detect errors, and respond quickly to incidents. This was a critical step in transitioning from basic deployment to real system operations, while also laying the groundwork for evaluation and improvement in the following weeks.
