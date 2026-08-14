---
title: "Cấu hình CloudWatch và kiểm thử Failover"
date : 2024-01-01
weight : 10
chapter : false
pre : " <b> 5.10. </b> "
---
Sau khi hoàn thành cấu hình Auto Scaling Group, bước tiếp theo là sử dụng Amazon CloudWatch để theo dõi hoạt động của hệ thống và thực hiện kiểm thử Failover. CloudWatch giúp giám sát các chỉ số như mức sử dụng CPU của EC2, trong khi quá trình Failover giúp kiểm tra khả năng tự động phục hồi của hệ thống khi một máy chủ gặp sự cố.

### 5.10.1. Cấu hình Amazon CloudWatch
#### Bước 1: Truy cập CloudWatch
1. Truy cập AWS Console.
2. Tìm kiếm và chọn CloudWatch.
3. Chọn All metrics.
4. Chọn EC2 để xem các chỉ số của EC2.

#### Bước 2: Theo dõi CPU của EC2

Trong CloudWatch → Metrics → All metrics → EC2 → Per-Instance Metrics, chọn các EC2 thuộc Auto Scaling Group.

Theo dõi chỉ số:
```
CPU Utilization
```
>Chỉ số này thể hiện mức sử dụng CPU của EC2 theo thời gian.

![alt text](/images/5-Workshop/5.10/5.10.1.png)
**Hình 5.10.1. Theo dõi chỉ số CPUUtilization của EC2**

#### Bước 3: Tạo CloudWatch Alarm

Để theo dõi khi CPU tăng cao:

1. Chọn Alarms → Create alarm.
2. Chọn metric CPUUtilization.
3. Chọn EC2 cần theo dõi.
4. Cấu hình điều kiện:
```
Metric: CPUUtilization
Threshold type: Static
Condition: Greater than
Threshold: 70%
```
5. Đặt tên:
```
workshop-high-cpu-alarm
```
6. Chọn Create alarm.

>Khi CPU vượt quá 70%, CloudWatch Alarm sẽ chuyển sang trạng thái In alarm.

![alt text](/images/5-Workshop/5.10/5.10.2.png)
**Hình 5.10.2. Cấu hình CloudWatch Alarm**

### 5.10.2. Kiểm thử Failover

Failover được thực hiện nhằm kiểm tra khả năng hệ thống tiếp tục hoạt động khi một EC2 gặp sự cố.

Trong Workshop, quá trình kiểm thử được thực hiện bằng cách Terminate một EC2 đang hoạt động trong Auto Scaling Group.

#### Bước 1: Kiểm tra trạng thái ban đầu

Trước khi thực hiện Failover, kiểm tra:

EC2 → Auto Scaling Groups → workshop-asg

Đảm bảo hệ thống đang có:
```
Desired capacity: 2
Minimum capacity: 2
Maximum capacity: 4
```
Kiểm tra Target Group:
```
EC2-01 → Healthy
EC2-02 → Healthy
```
![alt text](/images/5-Workshop/5.10/5.10.3.png)
**Hình 5.10.3. Trạng thái hệ thống trước khi kiểm thử Failover**

#### Bước 2: Terminate một EC2
1. Truy cập EC2 → Instances.
2. Chọn một EC2 thuộc Auto Scaling Group.
3. Chọn Instance state → Terminate instance.
4. Xác nhận Terminate.

Sau khi EC2 bị terminate, số lượng instance trong hệ thống sẽ tạm thời giảm xuống.

![alt text](/images/5-Workshop/5.10/5.10.5.png)
**Hình 5.10.5. Terminate EC2 để kiểm thử Failover**

#### Bước 3: Kiểm tra Auto Scaling

Quay lại:
```
EC2 → Auto Scaling Groups → workshop-asg → Activity
```
Auto Scaling sẽ phát hiện số lượng EC2 thấp hơn Desired capacity và tự động khởi tạo một EC2 mới.

Quá trình có thể được mô tả:
```
EC2-01 bị lỗi
      ↓
Auto Scaling phát hiện
      ↓
Khởi tạo EC2 mới
      ↓
EC2 mới được đưa vào Target Group
      ↓
Health Check
      ↓
Healthy
```
![alt text](/images/5-Workshop/5.10/5.10.6.png)
**Hình 5.10.6. Auto Scaling tự động khởi tạo EC2 thay thế**

#### Bước 4: Kiểm tra Target Group

Truy cập:
```
EC2 → Target Groups → workshop-tg → Targets
```
Kiểm tra trạng thái của các EC2.

Sau khi EC2 mới hoạt động, Target Group sẽ hiển thị:
```
EC2-02 → Healthy
EC2-03 → Healthy
```
Điều này cho thấy EC2 mới đã vượt qua Health Check và sẵn sàng nhận lưu lượng từ ALB.

**Hình 5.10.7. EC2 mới chuyển sang trạng thái Healthy**

#### Bước 5: Kiểm tra ứng dụng

Truy cập DNS Name của Application Load Balancer:
```
http://<ALB-DNS-Name>
```
Nếu ứng dụng vẫn truy cập được sau khi một EC2 bị terminate, quá trình Failover đã hoạt động thành công.

**Hình 5.10.8. Ứng dụng vẫn hoạt động sau khi Failover**

### 5.10.3. Đánh giá kết quả kiểm thử

Kết quả kiểm thử có thể được tổng hợp như sau:

| Nội dung kiểm thử                 | Kết quả     |
| --------------------------------- | ----------- |
| CloudWatch theo dõi CPU           | Thành công  |
| EC2 gặp sự cố                     | Đã kiểm thử |
| Auto Scaling phát hiện EC2 bị mất | Thành công  |
| EC2 mới được tạo                  | Thành công  |
| Target Group Health Check         | Healthy     |
| ALB tiếp tục phân phối request    | Thành công  |
| Ứng dụng tiếp tục hoạt động       | Thành công  |

Qua quá trình kiểm thử, hệ thống vẫn duy trì khả năng phục vụ người dùng khi một EC2 bị terminate. Auto Scaling tự động tạo EC2 thay thế, sau đó Target Group thực hiện Health Check trước khi đưa EC2 mới vào phục vụ.

