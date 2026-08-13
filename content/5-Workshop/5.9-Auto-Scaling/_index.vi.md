---
title: "Cấu hình Auto Scaling "
date : 2024-01-01
weight : 9
chapter : false
pre : " <b> 5.9. </b> "
---
Sau khi hoàn thành Launch Template và Application Load Balancer, bước tiếp theo là cấu hình Auto Scaling Group (ASG). Auto Scaling giúp hệ thống tự động điều chỉnh số lượng EC2 dựa trên nhu cầu sử dụng, đồng thời có khả năng tạo EC2 mới khi một máy chủ gặp sự cố.

Trong Workshop, Auto Scaling được cấu hình với mô hình ban đầu gồm 2 EC2, phân bố trên 2 Availability Zone và có thể mở rộng tối đa 4 EC2.
### 5.9.1. Tạo Auto Scaling Group
#### Bước 1: Truy cập Auto Scaling Groups
1. Truy cập AWS Console → EC2.
2. Trong menu bên trái, chọn Auto Scaling Groups.
3. Chọn Create Auto Scaling group.

![alt text](/images/5-Workshop/5.9/create-asg.png)
**Hình 5.9.1. Giao diện tạo Auto Scaling Group**

#### Bước 2: Đặt tên Auto Scaling Group

Tại phần Choose launch template or configuration:
```
Auto Scaling group name:
workshop-asg
```
Tại Launch template, chọn:
```
Launch Template:
workshop-launch-template
Version:
Latest
```
Sau đó chọn Next.
![alt text](/images/5-Workshop/5.9/launch-template.png)
**Hình 5.9.2. Lựa chọn Launch Template**

### 5.9.2. Cấu hình Network

Tại phần Network:

1. Chọn VPC đã tạo.
2. Tại Availability Zones and subnets, chọn các Subnet thuộc các Availability Zone khác nhau.

Việc lựa chọn nhiều Availability Zone giúp EC2 được phân bố trên nhiều khu vực độc lập, từ đó tăng khả năng chịu lỗi của hệ thống.
![alt text](/images/5-Workshop/5.9/network.png)
**Hình 5.9.3. Cấu hình Availability Zones và Subnets**

### 5.9.3. Gắn Auto Scaling với Target Group

Tại phần Configure advanced options:

1. Chọn:
```
Load balancing: Attach to an existing load balancer
```
2. Chọn Target Group đã tạo:
```
fca-web-target-group
```
3. Bật:
```
Turn on Elastic Load Balancing health checks
```
4. Cấu hình:
```
Health check grace period: 300 seconds
```
Health Check giúp Auto Scaling xác định EC2 có hoạt động bình thường hay không.

>Nếu một EC2 bị lỗi và liên tục ở trạng thái không khỏe mạnh, Auto Scaling có thể loại bỏ instance đó và tạo một instance mới thay thế.

### 5.9.4. Cấu hình Capacity

Tại phần Group size, cấu hình:
```
Desired capacity: 2
Minimum capacity: 2
Maximum capacity: 4
```
Ý nghĩa:
| Thông số | Giá trị | Ý nghĩa                  |
| -------- | ------: | ------------------------ |
| Desired  |       2 | Số EC2 mong muốn ban đầu |
| Minimum  |       2 | Không giảm dưới 2 EC2    |
| Maximum  |       4 | Không vượt quá 4 EC2     |

![alt text](/images/5-Workshop/5.9/group-size.png)
**Hình 5.9.4. Cấu hình Desired, Minimum và Maximum Capacity**

### 5.9.5. Thiết lập chính sách Scale Out / Scale In

Tại phần Configure group size and scaling, chọn chính sách mở rộng:
```
Scaling type:
Target tracking scaling policy
```
Chọn metric:
```
Average CPU utilization
```
Đặt giá trị mục tiêu:
```
Target value: 50%
```
Điều này có nghĩa là Auto Scaling sẽ cố gắng duy trì mức sử dụng CPU trung bình của các EC2 ở khoảng 50%.
```
CPU > 50%
     ↓
Scale Out
     ↓
2 EC2 → 3 EC2 → 4 EC2
```
Khi tải giảm:
```
CPU < 50%
     ↓
Scale In
     ↓
4 EC2 → 3 EC2 → 2 EC2
```

![alt text](/images/5-Workshop/5.9/scaling.png)
Hình 5.9.5. Cấu hình Target Tracking Scaling Policy
>Đối với Workshop, sử dụng Target Tracking là cách đơn giản để minh họa cơ chế tự động Scale Out và Scale In.

### 5.9.6. Hoàn tất Auto Scaling Group

Sau khi hoàn thành các cấu hình:

1. Kiểm tra Launch Template.
2. Kiểm tra VPC và Subnet.
3. Kiểm tra Target Group.
4. Kiểm tra Desired, Minimum và Maximum Capacity.
5. Kiểm tra Scaling Policy.
6. Chọn Create Auto Scaling group.