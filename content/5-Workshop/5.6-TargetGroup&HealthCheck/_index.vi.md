---
title: "Cấu hình Target Group và Health Check"
date : 2024-01-01
weight : 6
chapter : false
pre : " <b> 5.6. </b> "
---

Sau khi triển khai ứng dụng Python trên EC2, bước tiếp theo là tạo Target Group để quản lý các EC2 chạy ứng dụng. Target Group sẽ được sử dụng bởi Application Load Balancer (ALB) để phân phối lưu lượng đến các máy chủ. Đồng thời, Health Check giúp xác định EC2 nào đang hoạt động bình thường và sẵn sàng nhận request.

### 1. Tạo Target Group
#### Bước 1: Truy cập Target Groups
1. Truy cập AWS Console → EC2.
2. Trong menu bên trái, chọn Target Groups.
3. Chọn Create target group.
![target-group](/images/5-Workshop/5.6/target-group.png)
**Hình 5.6.1. Giao diện tạo Target Group**

#### Bước 2: Chọn loại Target

Tại Choose a target type, chọn:
```
Target type: Instances
```
Sau đó chọn Next.
#### Bước 3: Cấu hình Target Group

Thiết lập các thông số:
```
Target group name: workshop-tg
Protocol: HTTP
Port: 5000
IP address type: IPv4
VPC: fca-Workshop-vpc
Protocol version: HTTP1
```
Trong đó, Port 5000 là port mà ứng dụng Python Flask đang chạy trên EC2.

Ví dụ:
```
Application → 0.0.0.0:5000
Target Group → HTTP:5000
```
Sau đó chọn Next.

### 2. Đăng ký EC2 vào Target Group

Tại bước Register targets:

1. Chọn EC2 đã triển khai ứng dụng Python.
2. Kiểm tra port:
```
Port: 5000
```
3. Chọn Include as pending below.
4. Kiểm tra EC2 đã xuất hiện trong danh sách Review targets.
5. Chọn Create target group.
![ec2-to-target](/images/5-Workshop/5.6/ec2-to-targetgroup.png)
**Hình 5.6.2. Đăng ký EC2 vào Target Group**

Sau khi tạo, truy cập:

EC2 → Target Groups → workshop-tg → Targets

Có thể thấy EC2 đã được đăng ký vào Target Group.

### 3. Cấu hình Health Check

Health Check được sử dụng để kiểm tra tình trạng hoạt động của ứng dụng trên EC2.

#### Bước 1: Mở cấu hình Health Check
1. Chọn Target Groups.
2. Chọn ```workshop-tg.```
3. Chọn tab Health checks.
4. Chọn Edit health check settings.

#### Bước 2: Cấu hình Health Check

Thiết lập:
```
Health check protocol: HTTP
Health check path: /
Health check port: Traffic port
Healthy threshold: 2
Unhealthy threshold: 2
Timeout: 5 seconds
Interval: 30 seconds
Success codes: 200
```
Trong đó:

- Health check path /: ALB gửi request đến trang chính của ứng dụng.
- Success code 200: EC2 được xem là hoạt động bình thường khi ứng dụng trả về HTTP 200.
- Healthy threshold 2: cần 2 lần kiểm tra thành công liên tiếp để xác định EC2 hoạt động tốt.
- Unhealthy threshold 2: cần 2 lần kiểm tra thất bại liên tiếp để xác định EC2 không khỏe mạnh.

Chọn Save changes.

### 4. Kiểm tra trạng thái Target

Sau khi cấu hình Health Check:

1. Vào EC2 → Target Groups.
2. Chọn workshop-tg.
3. Chọn tab Targets.
4. Quan sát cột Status.

Nếu ứng dụng đang hoạt động bình thường, trạng thái sẽ chuyển thành:
```
healthy
```
![healthy](/images/5-Workshop/5.6/5.6.3.png)
**Hình 5.6.3. Target ở trạng thái Healthy**

Nếu trạng thái là unhealthy, cần kiểm tra:

- Ứng dụng Python có đang chạy hay không.
- Port ứng dụng có đúng 5000 hay không.
- Security Group có cho phép traffic đến port 5000 hay không.
- Health Check Path / có tồn tại hay không.

### 5. Kết quả 
Sau khi hoàn thành, hệ thống có Target Group quản lý EC2 và sử dụng Health Check để xác định trạng thái của ứng dụng.
```
                Target Group
                     │
              Health Check "/"
                     │
             ┌───────┴───────┐
             ▼               ▼
          EC2-01           EC2-02
           :5000             :5000
             │               │
          Healthy         Healthy
```
Target Group sẽ là thành phần trung gian giữa Application Load Balancer và các EC2. Khi triển khai nhiều EC2, ALB có thể chỉ gửi request đến những Target đang ở trạng thái Healthy, giúp tăng tính sẵn sàng của ứng dụng.