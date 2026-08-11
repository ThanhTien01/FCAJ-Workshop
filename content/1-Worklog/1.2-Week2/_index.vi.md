---
title: "Worklog Tuần 2"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.2. </b> "
---



### Mục tiêu tuần 2:

* Thiết kế kiến trúc hệ thống đảm bảo tính sẵn sàng cao trên AWS.
* Ứng dụng Multi-AZ và Load Balancer để giảm thiểu downtime và tăng khả năng chịu lỗi.
* Xác định thành phần dịch vụ AWS cần sử dụng trong giải pháp HA.

### Các công việc cần triển khai trong tuần này:
| Thứ | Công việc                                                                                                                                                                           | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu                            |
| --- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------ | --------------- | ----------------------------------------- |
| 2   | - Tổng hợp yêu cầu của bài tập và mục tiêu hệ thống HA <br> - Xác định thành phần kiến trúc phù hợp trên AWS                                                                       | 29/06/2026   | 29/06/2026      |
| 3   | - Nghiên cứu kiến trúc Multi-AZ cho EC2 và RDS <br> - Tìm hiểu cách hoạt động của Elastic Load Balancer (ALB/NLB) <br> - Xác định mô hình mạng VPC và subnet                        | 30/06/2026   | 30/06/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 4   | - Thiết kế sơ đồ hệ thống: <br>&emsp; + EC2 ở đa vùng Availability Zones <br>&emsp; + RDS Multi-AZ <br>&emsp; + S3 cho lưu trữ tĩnh <br>&emsp; + ELB cân bằng tải và săn lùng tình trạng | 01/07/2026   | 01/07/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 5   | - Xác định cấu hình mạng và bảo mật: <br>&emsp; + VPC, Subnet Public/Private <br>&emsp; + Route Table <br>&emsp; + Security Group <br>&emsp; + NACL và IAM role cho EC2/RDS        | 02/07/2026   | 02/07/2026      | <https://cloudjourney.awsstudygroup.com/> |
| 6   | - Chuẩn bị kế hoạch triển khai thử nghiệm: <br>&emsp; + Kiểm tra ưu tiên triển khai load balancer <br>&emsp; + Xác định phương án backup và recovery <br>&emsp; + So sánh chi phí | 03/07/2026   | 03/07/2026      | <https://cloudjourney.awsstudygroup.com/> |


### Kết quả đạt được tuần 2:

* Hiểu bài toán kiến trúc sẵn sàng cao và các yếu tố ảnh hưởng đến độ bền của hệ thống.
* Thiết kế được mô hình Multi-AZ cho EC2 với ít nhất hai Availability Zone để đảm bảo chịu lỗi khi một AZ gặp sự cố.
* Lên được kế hoạch sử dụng Elastic Load Balancer để phân phối lưu lượng và kiểm tra tình trạng instance.
* Xác định việc sử dụng RDS Multi-AZ để đảm bảo cơ sở dữ liệu luôn có bản sao dự phòng và tự động chuyển đổi khi cần.
* Nắm rõ cách tổ chức VPC với Subnet public/private, cấu hình Security Group và Route Table cho kiến trúc HA.
* Chuẩn bị được danh sách các dịch vụ AWS cần thiết cho kiến trúc: EC2, ELB, RDS Multi-AZ, S3, CloudWatch, IAM.
* Đã xác định các kịch bản kiểm thử failover và phương án giám sát cơ bản cho hệ thống.

### Bài học rút ra:

* Xây dựng kiến trúc sẵn sàng cao cần cân bằng giữa hiệu suất, độ bền và chi phí.
* Multi-AZ giúp giảm rủi ro do lỗi hạ tầng, trong khi Load Balancer đảm bảo cân bằng tải và phát hiện instance không hoạt động.
* Việc chuẩn bị mạng VPC, subnet và bảo mật là bước nền tảng quan trọng để hệ thống HA hoạt động ổn định.
* Kế hoạch triển khai rõ ràng sẽ giúp giảm sai sót khi bước sang giai đoạn thực hành thiết lập trên AWS.


