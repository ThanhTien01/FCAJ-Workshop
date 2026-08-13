---
title: "Cấu hình Amazon RDS và Amazon S3"
date : 2024-01-01
weight : 5
chapter : false
pre : " <b> 5.5. </b> "
---

Trong bước này, **Amazon RDS** được sử dụng để lưu trữ dữ liệu của ứng dụng, trong khi **Amazon S3** được sử dụng để lưu trữ các tệp và tài nguyên. Việc tách dữ liệu khỏi EC2 giúp ứng dụng dễ dàng mở rộng và quản lý hơn khi triển khai nhiều EC2.

### 1. Cấu hình Amazon RDS
#### Bước 1: Tạo Database
1. Truy cập AWS Console → RDS.
2. Chọn Databases → Create database.
3. Chọn:
- Creation method: Standard create.
- Engine: MySQL.
- Template: Free tier.
4. Tại phần Settings, nhập:
```
DB instance identifier: workshop-db
Master username: admin
Master password: ********
```
5. Tại phần Connectivity:
- Chọn VPC đã tạo.
- Chọn DB Subnet Group phù hợp.
- Không bật Public access nếu Database chỉ được sử dụng bởi EC2.
6. Tại VPC Security Group, chọn Security Group dành cho Database hoặc tạo mới.
7. Chọn Create database.
#### Bước 2. Cấu hình Security Group cho RDS
Để đảm bảo an toàn, Database chỉ cho phép EC2 kết nối đến MySQL.

Cấu hình Inbound Rule:
```
Type: MySQL/Aurora
Protocol: TCP
Port: 3306
Source: Security Group của EC2 
```
Không nên mở port 3306 cho toàn bộ Internet.
#### Bước 3. 
Kiểm tra RDS

Sau khi Database chuyển sang trạng thái Available, chọn Database và lấy:
```
Endpoint
Port
```
Ví dụ:
```
Endpoint: workshop-db.xxxxx.ap-southeast-1.rds.amazonaws.com
Port: 3306
```
Endpoint này sẽ được sử dụng để cấu hình kết nối Database cho ứng dụng Python.
![rds](/images/5-Workshop/5.5/rds.png)
**Hình RDS đã được tạo**

### 2. Cấu hình Amazon S3 
Amazon S3 được sử dụng để lưu trữ các tệp hoặc tài nguyên của ứng dụng như hình ảnh, file upload hoặc các dữ liệu tĩnh.

#### Bước 1: Tạo S3 Bucket
1. Truy cập AWS Console → S3.
2. Chọn Create bucket.
3. Đặt tên Bucket duy nhất.
```
workshop-high-availability-<unique-id>
```
4. Chọn AWS Region giống với Region đang sử dụng.
5. Giữ Block all public access được bật.
6. Chọn Create bucket.

#### Bước 2: Upload dữ liệu
1. Mở Bucket vừa tạo.
2. Chọn Upload.
3. Chọn file hoặc thư mục cần lưu trữ.
4. Chọn Upload.

Sau khi upload, các file sẽ được lưu trữ trên Amazon S3 thay vì lưu trực tiếp trên EC2.

#### Bước 3: Kiểm tra Bucket

Kiểm tra:

- Bucket được tạo thành công.
- File đã được upload.
- Bucket đang ở đúng Region.
- Quyền truy cập được cấu hình phù hợp.

![s3](/images/5-Workshop/5.5/rds.png)
**Hình ảnh Amazon S3 đã được tạo**

### Kết quả

Sau khi hoàn thành bước này, hệ thống có thể được tổ chức như sau:
```

                  Python Web Application
                           │
                 ┌─────────┴─────────┐
                 ▼                   ▼
            Amazon RDS           Amazon S3
            Database             File Storage
```
Việc sử dụng RDS cho Database và S3 cho File Storage giúp tách dữ liệu khỏi EC2. Khi Auto Scaling tạo thêm EC2 mới, các instance có thể sử dụng chung Database và dữ liệu được lưu trữ tập trung, phù hợp với mục tiêu xây dựng hệ thống High Availability.