---
title: "Workshop"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5. </b> "
---

# ĐẢM BẢO TÍNH SẴN SÀNG CAO TRÊN AWS 
#### Tổng quan

Trong môi trường Cloud, việc đảm bảo hệ thống có thể hoạt động ổn định và liên tục là một trong những yêu cầu quan trọng đối với các ứng dụng và dịch vụ trực tuyến. Khi một máy chủ hoặc một thành phần của hệ thống gặp sự cố, nếu hệ thống không có cơ chế dự phòng, ứng dụng có thể bị gián đoạn và ảnh hưởng trực tiếp đến người dùng.

Đề tài “Đảm bảo tính sẵn sàng cao (High Availability) trên AWS” tập trung vào việc thiết kế và triển khai một hệ thống Web Application có khả năng duy trì hoạt động, chịu lỗi và tự động phục hồi khi xảy ra sự cố. Hệ thống được triển khai trên nhiều Availability Zone nhằm hạn chế Single Point of Failure và tăng khả năng hoạt động liên tục.

Trong Workshop, ứng dụng được triển khai trên Amazon EC2 và sử dụng Application Load Balancer (ALB) để phân phối lưu lượng đến các máy chủ. Auto Scaling được sử dụng để tự động điều chỉnh số lượng máy chủ dựa trên nhu cầu sử dụng, đồng thời hỗ trợ thay thế các máy chủ gặp sự cố. Đối với dữ liệu, hệ thống có thể sử dụng Amazon RDS Multi-AZ nhằm tăng khả năng dự phòng cho cơ sở dữ liệu.

Bên cạnh đó, Amazon CloudWatch được sử dụng để theo dõi trạng thái và hiệu năng của hệ thống, từ đó hỗ trợ phát hiện các vấn đề và đưa ra cảnh báo khi cần thiết.

Thông qua đề tài, người thực hiện có cơ hội tìm hiểu và thực hành các nguyên tắc quan trọng trong việc xây dựng hệ thống High Availability trên AWS, từ thiết kế kiến trúc, triển khai ứng dụng, phân phối lưu lượng, tự động mở rộng cho đến kiểm thử khả năng chịu lỗi. Qua đó, đề tài giúp minh họa cách AWS có thể được sử dụng để xây dựng các hệ thống có tính ổn định, khả năng mở rộng và khả năng phục hồi cao.

#### Nội dung

1. [Tổng quan về workshop](5.1-Workshop-overview/)
2. [Chuẩn bị](5.2-Prerequiste/)
3. [Cấu hình mạng AWS](5.3-Configure-the-AWS-Network/)
4. [Triển khai ứng dụng Web Python](5.4-Deloy-Python)
5. [Cấu hình Amazon RDS và Amazon S3](5.5-Configure-RDS&S3)
6. [Cấu hình Target Group và Health Check](5.6-TargetGroup&HealthCheck)
7. [Cấu hình Application Load Balancer](5.7-Auto-Load-Balancer)
8. [Cấu hình Launch Template](5.8-Launch-Template)
9. [Cấu hình Auto Scaling](5.9-Auto-Scaling)
10. [Cấu hình CloudWatch](5.10-CloudWatch)
11. [Dọn dẹp tài nguyên](5.11-Cleanup)
12. [Kết quả và kết luận](5.12-Result-Conclusion)