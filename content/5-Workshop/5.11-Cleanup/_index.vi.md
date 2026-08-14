---
title : "Dọn dẹp tài nguyên"
date : 2024-01-01
weight : 11
chapter : false
pre : " <b> 5.11. </b> "
---
Sau khi hoàn thành Workshop và kiểm thử khả năng High Availability, cần tiến hành dọn dẹp các tài nguyên AWS đã tạo. Việc này giúp tránh phát sinh chi phí không cần thiết và đảm bảo tài khoản AWS không còn các tài nguyên đang chạy sau khi kết thúc Workshop.

### 5.11.1. Xóa Auto Scaling Group

Truy cập:

AWS Console → EC2 → Auto Scaling Groups

1. Chọn workshop-asg.
2. Chọn Delete.
3. Xác nhận xóa Auto Scaling Group.
4. Kiểm tra các EC2 do Auto Scaling quản lý đã được xử lý.

**Hình 5.11.1. Xóa Auto Scaling Group**

### 5.11.2. Xóa Application Load Balancer

Truy cập:

EC2 → Load Balancers

1. Chọn workshop-alb.
2. Chọn Actions → Delete load balancer.
3. Xác nhận Delete.

>Sau khi xóa, kiểm tra danh sách Load Balancer để đảm bảo workshop-alb không còn tồn tại.

**Hình 5.11.2. Xóa Application Load Balancer**

### 5.11.3. Xóa Target Group

Truy cập:

EC2 → Target Groups

1. Chọn workshop-tg.
2. Chọn Actions → Delete.
3. Xác nhận xóa Target Group.

**Hình 5.11.3. Xóa Target Group**

### 5.11.4. Xóa Launch Template

Truy cập:

EC2 → Launch Templates

1. Chọn workshop-launch-template.
2. Chọn Actions → Delete template.
3. Xác nhận xóa.

>Launch Template không phát sinh chi phí trực tiếp, tuy nhiên nên xóa để tránh để lại các cấu hình không cần thiết.

**Hình 5.11.4. Xóa Launch Template**

### 5.11.5. Xóa Amazon RDS

Nếu Workshop đã tạo Database RDS và không còn sử dụng:

1. Truy cập AWS Console → RDS.
2. Chọn Databases.
3. Chọn Database workshop-db.
4. Chọn Actions → Delete.
5. Tắt tùy chọn tạo final snapshot nếu Database chỉ được sử dụng cho Workshop và không cần giữ dữ liệu.
6. Xác nhận xóa Database.

**Hình 5.11.5. Xóa Amazon RDS**

>Cần kiểm tra kỹ trước khi xóa vì thao tác này có thể làm mất dữ liệu Database.

### 5.11.6. Xóa dữ liệu trên Amazon S3

Nếu không cần sử dụng Bucket sau Workshop:

1. Truy cập AWS Console → S3.
2. Chọn Bucket đã tạo.
3. Chọn Empty để xóa toàn bộ dữ liệu.
4. Xác nhận xóa dữ liệu.
5. Chọn Bucket → Delete.
6. Nhập tên Bucket để xác nhận.

**Hình 5.11.6. Xóa Amazon S3 Bucket**

### 5.11.7. Xóa các tài nguyên mạng

Sau khi các tài nguyên phụ thuộc đã được xóa, tiến hành xóa các thành phần mạng:

- Security Groups không còn sử dụng.
- Route Tables không còn sử dụng.
- Internet Gateway.
- Subnets.
- VPC.

Thực hiện tại:
```
AWS Console → VPC
```

**Hình 5.11.7. Dọn dẹp các tài nguyên mạng**

>Cần xóa các tài nguyên phụ thuộc trước. Ví dụ, không thể xóa VPC khi bên trong vẫn còn EC2, Load Balancer hoặc các tài nguyên mạng đang sử dụng.

### 5.11.8. Kiểm tra và hoàn tất

Sau khi dọn dẹp, kiểm tra lại các dịch vụ:
| Dịch vụ                   | Trạng thái               |
| ------------------------- | ------------------------ |
| EC2                       | Đã Terminate             |
| Auto Scaling Group        | Đã xóa                   |
| Application Load Balancer | Đã xóa                   |
| Target Group              | Đã xóa                   |
| Launch Template           | Đã xóa                   |
| Amazon RDS                | Đã xóa                   |
| Amazon S3                 | Đã xóa                   |
| VPC và Network            | Đã xóa nếu không sử dụng |
| CloudWatch Alarm          | Đã xóa                   |

>Cuối cùng, có thể truy cập AWS Billing and Cost Management để kiểm tra xem còn tài nguyên nào đang phát sinh chi phí hay không.