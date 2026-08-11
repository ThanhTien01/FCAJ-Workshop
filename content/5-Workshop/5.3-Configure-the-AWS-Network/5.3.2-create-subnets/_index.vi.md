---
title : "Tạo Subnet"
date : 2024-01-01 
weight : 2
chapter : false
pre : " <b> 5.3.2 </b> "
---

Sau khi tạo VPC, hai subnet được tạo tại các **Availability Zone** khác nhau.

Việc phân bố subnet trên nhiều Availability Zone tạo nền tảng mạng cho việc triển khai các tài nguyên ứng dụng với khả năng sẵn sàng và khả năng chịu lỗi tốt hơn.

Các subnet được tạo bên trong `fca-workshop-vpc`:

| Subnet | Availability Zone | IPv4 CIDR |
|---|---|---|
| `fca-public-subnet-a` | `ap-southeast-1a` | `10.0.1.0/24` |
| `fca-public-subnet-b` | `ap-southeast-1b` | `10.0.2.0/24` |

Subnet thứ nhất được tạo tại `ap-southeast-1a` với CIDR `10.0.1.0/24`.

Subnet thứ hai được tạo tại `ap-southeast-1b` với CIDR `10.0.2.0/24`.

Sau khi tạo xong hai subnet, kiểm tra lại cấu hình tại **VPC → Subnets**.

**Hình 5.4. Các Subnet được phân bố trên hai Availability Zone**
![Các Subnet được phân bố trên hai Availability Zone](/images/5-Workshop/5.3-Configure-the-AWS-Network/subnets-created.png)