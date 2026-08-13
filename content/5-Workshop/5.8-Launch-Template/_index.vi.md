---
title: "Cấu hình Launch Template "
date : 2024-01-01
weight : 8
chapter : false
pre : " <b> 5.8. </b> "
---
Sau khi hoàn thành cấu hình Application Load Balancer, bước tiếp theo là tạo Launch Template. Launch Template lưu trữ các thông tin cấu hình cần thiết để khởi tạo EC2 mới, chẳng hạn như AMI, Instance Type, Key Pair và Security Group.

Launch Template sẽ được sử dụng bởi Auto Scaling Group để tự động tạo các EC2 có cấu hình giống nhau. Đây là thành phần quan trọng giúp hệ thống có khả năng mở rộng và tự động phục hồi khi một EC2 gặp sự cố.
### 5.8.1. Tạo Launch Template
#### Bước 1: Truy cập Launch Templates
1. Truy cập AWS Console → EC2.
2. Trong menu bên trái, chọn Launch Templates.
3. Chọn Create launch template.

![alt text](/images/5-Workshop/5.8/5.8.1.png)
**Hình 5.8.1. Giao diện tạo Launch Template**

#### Bước 2: Cấu hình thông tin Launch Template

Tại phần Launch template name and description, nhập:
```
Launch template name: workshop-launch-template
Description: Launch Template for High Availability Workshop
```
### 5.8.2. Chọn Amazon Machine Image

Tại phần Application and OS Images (Amazon Machine Image):

1. Chọn Quick Start.
2. Chọn Ubuntu.
3. Chọn phiên bản Ubuntu đang sử dụng cho EC2 trước đó.
```
AMI: Ubuntu Server 24.04 LTS
Architecture: 64-bit (x86)
```
Nên sử dụng cùng AMI với EC2 đã triển khai ứng dụng trước đó để đảm bảo các EC2 được Auto Scaling tạo ra có môi trường tương đồng.
![alt text](/images/5-Workshop/5.8/5.8.2.png)
**Hình 5.8.2. Lựa chọn AMI cho Launch Template**
#### 5.8.3. Cấu hình Instance Type và Key Pair

Tại phần Instance type, chọn cấu hình nhỏ phù hợp với Workshop:
```
Instance type: t3.micro
```
Tại Key pair, chọn Key Pair đã tạo trước đó:
```
Key pair: fca-workshop-key
```
Key Pair được sử dụng để kết nối và quản trị EC2 khi cần thiết.
![alt text](/images/5-Workshop/5.8/5.8.3.png)
**Hình 5.8.3. Cấu hình Instance Type và Key Pair**
### 5.8.4. Cấu hình Security Group

Tại phần Network settings, chọn Security Group dành cho EC2.

```
Security Group: workshop-sg
```
Security Group này cần cho phép các kết nối cần thiết từ hệ thống.

Trong kiến trúc hoàn chỉnh, nên cấu hình:
```
ALB Security Group
        │
        │ HTTP : 5000
        ▼
EC2 Security Group
```
Thay vì cho phép Internet truy cập trực tiếp vào port ứng dụng.

![alt text](/images/5-Workshop/5.8/5.8.4.png)

**Hình 5.8.4. Cấu hình Security Group**
### 5.8.5. Cấu hình User Data

Để các EC2 được tạo tự động có thể chạy ứng dụng Python, có thể sử dụng User Data để tự động cài đặt môi trường và khởi chạy ứng dụng khi EC2 được tạo.

Tại Advanced details → User data, nhập script phù hợp với ứng dụng.
![alt text](/images/5-Workshop/5.8/5.8.5.png)

**Hình 5.8.5. Cấu hình User Data**
### 5.8.6. Tạo Launch Template

Sau khi hoàn thành các cấu hình:

1. Kiểm tra lại AMI.
2. Kiểm tra Instance Type.
3. Kiểm tra Key Pair.
4. Kiểm tra Security Group.
5. Kiểm tra User Data.
6. Chọn Create launch template.

Sau khi tạo thành công, Launch Template sẽ xuất hiện trong danh sách:
```
workshop-launch-template
Version: 1
```
![alt text](/images/5-Workshop/5.8/5.8.6.png)
**Hình 5.8.6. Launch Template được tạo thành công**