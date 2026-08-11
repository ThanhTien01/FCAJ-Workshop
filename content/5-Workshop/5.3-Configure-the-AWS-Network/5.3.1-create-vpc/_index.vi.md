---
title : "Tạo VPC"
date : 2024-01-01 
weight : 1
chapter : false
pre : " <b> 5.3.1 </b> "
---

### 5.3.1. Tạo VPC

Bước đầu tiên trong quá trình xây dựng hạ tầng mạng AWS là tạo một **Amazon Virtual Private Cloud (VPC)**.

VPC cung cấp một mạng ảo riêng biệt cho các tài nguyên AWS được sử dụng trong workshop. Các tài nguyên của ứng dụng sẽ được triển khai bên trong VPC này ở các bước tiếp theo.

Truy cập:

**AWS Management Console → VPC → Your VPCs → Create VPC**

Tại mục **Resources to create**, chọn:

**VPC only**

Cấu hình VPC như sau:

| Cấu hình | Giá trị |
|---|---|
| **Name tag** | `fca-workshop-vpc` |
| **IPv4 CIDR block** | `10.0.0.0/16` |
| **IPv6 CIDR block** | No IPv6 CIDR block |
| **Tenancy** | Default |

Sau khi hoàn tất cấu hình, chọn **Create VPC**.

Kiểm tra VPC vừa tạo tại **Your VPCs**. VPC phải có trạng thái **Available** và hiển thị đúng IPv4 CIDR đã cấu hình.

**Hình 5.3. Cấu hình VPC**
![VPC Configuration](/images/5-workshop/5.3-Configure-the-AWS-Network/vpc-created.png)