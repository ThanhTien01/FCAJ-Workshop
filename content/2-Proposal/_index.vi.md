---
title: "Bản đề xuất"
date: 2024-01-01
weight: 2
chapter: false
pre: " <b> 2. </b> "
---
# High Availability on AWS 
## Đảm bảo tính sẵn sàng cao trên AWS 
## 1. Tóm tắt vấn đề

Trong các hệ thống Web Application, việc ứng dụng phụ thuộc vào một máy chủ hoặc một Availability Zone duy nhất có thể dẫn đến tình trạng gián đoạn dịch vụ khi máy chủ gặp sự cố, lưu lượng truy cập tăng cao hoặc xảy ra lỗi hạ tầng.

Workshop này đề xuất xây dựng một hệ thống Web Application trên AWS theo mô hình High Availability, trong đó ứng dụng được triển khai trên nhiều Amazon EC2 thuộc các Availability Zone khác nhau. Application Load Balancer được sử dụng để phân phối lưu lượng, Auto Scaling đảm bảo khả năng tự động mở rộng và thay thế máy chủ khi cần thiết, Amazon RDS Multi-AZ cung cấp khả năng dự phòng cho cơ sở dữ liệu và Amazon CloudWatch được sử dụng để giám sát hệ thống.

Mục tiêu của Workshop là xây dựng một mô hình có khả năng duy trì hoạt động, chịu lỗi và tự động phục hồi khi một thành phần trong hệ thống gặp sự cố.

## 2. Tuyên bố vấn đề

Hệ thống ứng dụng Web nếu chỉ triển khai trên một EC2 sẽ tồn tại Single Point of Failure. Khi EC2 gặp sự cố, toàn bộ ứng dụng có thể không thể truy cập được.

Ngoài ra, khi lượng truy cập tăng cao, một máy chủ duy nhất có thể không đủ khả năng xử lý lưu lượng. Việc mở rộng máy chủ thủ công cũng làm tăng thời gian phản hồi và yêu cầu quản trị.

Đối với cơ sở dữ liệu, nếu chỉ sử dụng một Database Instance duy nhất thì sự cố tại Database cũng có thể làm gián đoạn toàn bộ ứng dụng.

Do đó, Workshop tập trung giải quyết các vấn đề:

- Loại bỏ Single Point of Failure ở tầng ứng dụng.
- Đảm bảo ứng dụng có thể hoạt động khi một EC2 gặp sự cố.
- Tự động mở rộng hệ thống khi tải tăng.
- Tự động thay thế EC2 bị lỗi.
- Tăng tính sẵn sàng của cơ sở dữ liệu.
- Theo dõi và phát hiện các vấn đề của hệ thống.

## 3. Kiến trúc giải pháp

Giải pháp được xây dựng trên AWS theo mô hình triển khai trên hai Availability Zone.

**Hình kiến trúc còn thiếu**

| Thành phần | Vai trò |
|---|---|
| Amazon VPC | Xây dựng môi trường mạng |
| Public/Private Subnet | Phân tách tài nguyên mạng |
| EC2 | Chạy ứng dụng Python |
| Docker | Đóng gói ứng dụng |
| Amazon ECR | Lưu trữ Docker Image |
| Application Load Balancer | Phân phối lưu lượng |
| Auto Scaling | Tự động mở rộng và thay thế EC2 |
| Amazon RDS Multi-AZ | Dự phòng Database |
| CloudWatch | Monitoring và cảnh báo |

Luồng hoạt động chính: 
``` text 
User
↓
Application Load Balancer
↓
EC2 ở AZ-A / EC2 ở AZ-B
↓
Application
↓
RDS Multi-AZ
```

## 4. Triển khai kỹ thuật

*Các bước triển khai chính:*
1. Thiết kế VPC, subnet, security group và IAM role phù hợp.
2. Triển khai các EC2 instance chạy ứng dụng Python.
3. Tạo và cấu hình Application Load Balancer cùng target group.
4. Cấu hình Auto Scaling Group với chính sách scale-out và scale-in dựa trên CPU hoặc request.
5. Triển khai Amazon RDS cho cơ sở dữ liệu, cấu hình backup và bảo trì.
6. Sử dụng Amazon S3 để lưu trữ nội dung tĩnh và dữ liệu sao lưu.
7. Thiết lập CloudWatch metrics, alarms và log để giám sát CPU, latency, error rate.
8. Kiểm thử failover bằng cách tắt một instance EC2 và quan sát ALB/ASG phản hồi.

## 5. Lộ trình và mốc triển khai

| Tuần | Nội dung | Kết quả |
|---|---|---|
| Tuần 1 | Tìm hiểu High Availability và các dịch vụ AWS | Hiểu kiến thức nền tảng |
| Tuần 2 | Thiết kế kiến trúc Multi-AZ | Hoàn thành kiến trúc hệ thống |
| Tuần 3 | Chuẩn bị Python, Docker và ECR | Ứng dụng chạy bằng Docker |
| Tuần 4 | Xây dựng VPC, EC2 và RDS | Hệ thống cơ bản hoạt động |
| Tuần 5 | Cấu hình ALB và Auto Scaling | Hoàn thành khả năng Load Balancing và Scaling |
| Tuần 6 | Cấu hình CloudWatch | Hoàn thành Monitoring |
| Tuần 7 | Kiểm thử Failover và Auto Scaling | Xác nhận khả năng chịu lỗi |
| Tuần 8 | Đánh giá, tối ưu và hoàn thiện báo cáo | Hoàn thiện Workshop và báo cáo |

*Các mốc quan trọng*

Mốc 1: Ứng dụng Python chạy thành công trên EC2.

Mốc 2: ALB phân phối request đến nhiều EC2.

Mốc 3: Auto Scaling hoạt động.

Mốc 4: RDS Multi-AZ hoạt động.

Mốc 5: CloudWatch Monitoring hoàn thành.

Mốc 6: Kiểm thử EC2 failure thành công.

Mốc 7: Hoàn thiện báo cáo.
## 6. Ước tính ngân sách

*Chi phí hạ tầng*
- Amazon EC2: 1,50 USD/tháng (2 instance cấu hình nhỏ).
- Application Load Balancer: 1,50 USD/tháng (1 ALB).
- Amazon RDS: 2,00 USD/tháng (MySQL cấu hình nhỏ).
- Amazon EBS: 0,50 USD/tháng (lưu trữ).
- Amazon ECR: 0,10 USD/tháng (Docker Image).
- Amazon CloudWatch: 0,20 USD/tháng (monitoring).
- Truyền dữ liệu: 0,20 USD/tháng (lưu lượng thấp).

Tổng: khoảng 6,00 USD/tháng, 48,00 USD/8 tháng.
## 7. Đánh giá rủi ro

| Rủi ro | Mức độ | Giải pháp |
|---|---|---|
| EC2 gặp sự cố | Cao | Sử dụng nhiều EC2 và Auto Scaling |
| Một AZ gặp sự cố | Cao | Phân bố EC2 trên nhiều AZ |
| ALB không nhận được request | Trung bình | Kiểm tra Listener, Security Group và Target Group |
| EC2 ở trạng thái Unhealthy | Cao | Cấu hình Health Check chính xác |
| Auto Scaling không tạo EC2 | Cao | Kiểm tra Launch Template, IAM Role và Subnet |
| Database gặp sự cố | Cao | Sử dụng RDS Multi-AZ |
| CPU tăng cao | Trung bình | Cấu hình Auto Scaling Policy |
| Cấu hình Security Group sai | Cao | Chỉ mở các port cần thiết |
| Docker Container không chạy | Trung bình | Kiểm tra Docker Image, ECR và User Data |
| Cấu hình sai mạng | Trung bình | Kiểm tra Route Table, Subnet và Internet Gateway |

>Ngoài ra, trong quá trình thực hiện cần thường xuyên kiểm tra AWS Billing để tránh phát sinh chi phí ngoài dự kiến.
## 8. Kết quả kỳ vọng

Kết quả mong đợi:
- Hệ thống web hoạt động liên tục ngay cả khi một instance hoặc một AZ gặp sự cố.
- Traffic phân phối đều qua ALB và ASG tự động điều chỉnh quy mô.
- Dữ liệu lưu trữ an toàn trên RDS và S3.
- Giám sát CloudWatch cung cấp cảnh báo kịp thời.
- Có kịch bản kiểm thử failover và báo cáo đánh giá hiệu quả của giải pháp.
