---
title : "Các bước chuẩn bị"
date : 2024-01-01 
weight : 2
chapter : false
pre : " <b> 5.2. </b> "
---
## 5.2. Điều kiện tiên quyết

Trước khi bắt đầu triển khai, cần chuẩn bị môi trường AWS và các tài nguyên ứng dụng cần thiết. Các điều kiện này là nền tảng để triển khai ứng dụng Web Python và xây dựng kiến trúc High Availability.

### 5.2.1. Tài khoản AWS và Region

Cần có một **tài khoản AWS đang hoạt động** để tạo và quản lý các tài nguyên AWS được sử dụng trong workshop.

AWS Region được lựa chọn trước khi tạo các tài nguyên. Trong workshop này, Region được sử dụng là:

**AWS Region:** `ap-southeast-1`  
**Region:** Asia Pacific (Singapore)

Region được lựa chọn cung cấp nhiều **Availability Zones (AZs)**, được sử dụng trong các bước tiếp theo để phân bố các EC2 instance và nâng cao tính sẵn sàng của hệ thống.

**Hình 5.1. Các Availability Zone khả dụng**
![Available Availability Zones](/images/5-Workshop/5.2-Prerequisite/availability-zones.png) 

### 5.2.2. EC2 Key Pair

Một **EC2 Key Pair** được chuẩn bị để phục vụ việc truy cập an toàn vào các EC2 instance sẽ được tạo trong workshop.

Key Pair được tạo tại:

**EC2 → Network & Security → Key Pairs → Create key pair**

Private Key được lưu trữ an toàn và sẽ được sử dụng khi kết nối đến EC2 instance.

**Hình 5.2. EC2 Key Pair**
![EC2 Key Pair](/images/5-Workshop/5.2-Prerequisite/ec2-key-pair.png)

### 5.2.3. Ứng dụng Web Python

Workshop yêu cầu một ứng dụng Web được xây dựng bằng **Python**. Ứng dụng sẽ được triển khai trên Amazon EC2 và được sử dụng để kiểm tra hoạt động của Application Load Balancer và Auto Scaling.

Để dễ dàng kiểm tra hoạt động của Load Balancer, ứng dụng sẽ hiển thị thông tin xác định EC2 instance đang xử lý request, chẳng hạn như **Hostname** và **Instance ID**.

Source code của ứng dụng được chuẩn bị trước khi bắt đầu triển khai.

**Hình 5.3. Source Code của ứng dụng Web Python**
![Source Code của ứng dụng Web Python](/images/5-Workshop/5.2-Prerequisite/python-project.png)

### 5.2.4. Kiểm tra điều kiện tiên quyết

Trước khi chuyển sang phần triển khai, các điều kiện sau được kiểm tra:

| Điều kiện | Trạng thái |
|---|---|
| Tài khoản AWS | Đã sẵn sàng |
| AWS Region | `ap-southeast-1` |
| Availability Zones | Có sẵn |
| EC2 Key Pair | Đã tạo |
| Python Web Application | Đã chuẩn bị |

Sau khi hoàn thành các điều kiện trên, môi trường đã sẵn sàng để bắt đầu cấu hình hạ tầng mạng AWS.