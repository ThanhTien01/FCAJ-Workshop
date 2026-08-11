---
title: "Worklog Tuần 5"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.5. </b> "
---


### Mục tiêu tuần 5:

* Tìm hiểu và triển khai Application Load Balancer để phân phối lưu lượng cho hệ thống.
* Thiết lập Auto Scaling Group nhằm tăng tính sẵn sàng và khả năng chịu tải của ứng dụng.
* Kiểm tra độ ổn định của hệ thống khi có thay đổi về số lượng instance và mức traffic.
* Nắm rõ quy trình cấu hình target group, health check, scale-out và scale-in policy.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Tìm hiểu kiến trúc Load Balancer trên AWS <br> - So sánh ALB với các mô hình cân bằng tải khác | 20/07/2026 | 20/07/2026 | <https://aws.amazon.com/elasticloadbalancing/> |
| 3 | - Tạo target group cho EC2 instance <br> - Thiết lập health check và trạng thái healthy/unhealthy | 21/07/2026 | 21/07/2026 | <https://aws.amazon.com/elasticloadbalancing/> |
| 4 | - Triển khai Application Load Balancer <br> - Cấu hình listener, port, protocol và routing | 22/07/2026 | 22/07/2026 | <https://aws.amazon.com/elasticloadbalancing/> |
| 5 | - Tạo Auto Scaling Group <br> - Thiết lập launch template và min/max/desired capacity | 23/07/2026 | 23/07/2026 | <https://aws.amazon.com/autoscaling/> |
| 6 | - Cấu hình policy scale-out / scale-in dựa trên CPU <br> - Kiểm thử tăng giảm số lượng instance và đánh giá hiệu quả | 24/07/2026 | 24/07/2026 | <https://aws.amazon.com/autoscaling/> |

### Kết quả đạt được tuần 5:

* Hiểu rõ vai trò của Application Load Balancer trong việc phân phối lưu lượng và nâng cao tính sẵn sàng của hệ thống.
* Thiết lập thành công target group và health check để ALB có thể xác định trạng thái của EC2 instance.
* Triển khai được ALB trên AWS và cấu hình listener để chuyển tiếp request tới ứng dụng.
* Nắm được cách Auto Scaling Group hoạt động theo quy mô instance và khả năng thay thế tự động khi có lỗi xảy ra.
* Tạo launch template để chuẩn hóa cấu hình EC2 khi Auto Scaling mở rộng hoặc tái tạo instance.
* Cấu hình thành công chính sách scale-out và scale-in dựa trên mức độ sử dụng CPU hoặc metrics hệ thống.
* Thực hiện kiểm thử việc tăng số lượng instance khi tải cao và giảm số lượng khi tải giảm xuống.
* Nhận thấy rõ hiệu quả của Load Balancer và Auto Scaling trong việc cải thiện độ ổn định, tăng khả năng chịu tải và giảm nguy cơ downtime.

### Bài học rút ra:

* Load Balancer giúp phân phối lưu lượng đồng đều, tránh tình trạng một instance bị quá tải và nâng cao tính khả dụng cho ứng dụng.
* Health check là yếu tố quan trọng để ALB biết instance nào đang hoạt động ổn định và instance nào cần loại bỏ khỏi vòng phân phối.
* Auto Scaling là giải pháp hiệu quả cho việc mở rộng tài nguyên theo nhu cầu thực tế, giúp tối ưu chi phí và tăng tính linh hoạt.
* Khi cấu hình Auto Scaling, cần xác định rõ min, max và desired capacity để tránh việc mở rộng quá mức hoặc không đủ tài nguyên khi có tải cao.
* Việc kiểm thử chính sách scale-out/scale-in giúp đánh giá mức độ phản hồi của hệ thống trước các tình huống thay đổi lưu lượng thực tế.

### Đánh giá chung:

Tuần 5 là giai đoạn quan trọng trong quá trình triển khai hệ thống khi tôi chuyển từ việc chạy ứng dụng trên một EC2 đơn lẻ sang mô hình có tính sẵn sàng cao hơn. Với việc cấu hình Load Balancer và Auto Scaling, hệ thống đã có khả năng phân phối lưu lượng và tự điều chỉnh theo tải. Đây là bước nâng cấp rất quan trọng, giúp hệ thống gần hơn với kiến trúc High Availability và tạo nền tảng cho các tuần tiếp theo về giám sát, failover và tối ưu hóa hiệu suất.

