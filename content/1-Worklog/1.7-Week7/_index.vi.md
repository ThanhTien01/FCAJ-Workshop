---
title: "Worklog Tuần 7"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.7. </b> "
---



### Mục tiêu tuần 7:

* Kiểm tra khả năng chịu lỗi của hệ thống bằng các kịch bản failover thực tế.
* Giả lập sự cố ở instance EC2 và đánh giá phản hồi của Load Balancer, Auto Scaling và hệ thống ứng dụng.
* Xác nhận tính sẵn sàng của hệ thống sau khi có lỗi xảy ra ở một thành phần.
* Thu thập dữ liệu và đánh giá hiệu quả của kiến trúc High Availability.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Lập kế hoạch thử nghiệm failover và xác định các kịch bản sự cố cần giả lập | 03/08/2026 | 03/08/2026 | <https://aws.amazon.com/ec2/> |
| 3 | - Giả lập lỗi EC2 instance bằng cách ngừng hoạt động instance hoặc tắt máy ảo | 04/08/2026 | 04/08/2026 | <https://aws.amazon.com/ec2/> |
| 4 | - Theo dõi trạng thái của ALB, target group và Auto Scaling Group trong quá trình failover | 05/08/2026 | 05/08/2026 | <https://aws.amazon.com/elasticloadbalancing/> |
| 5 | - Kiểm tra ứng dụng sau khi instance bị mất và xác nhận hệ thống tiếp tục phục vụ người dùng | 06/08/2026 | 06/08/2026 | <https://aws.amazon.com/autoscaling/> |
| 6 | - Tổng hợp kết quả, đánh giá độ trễ, thời gian phục hồi và hiệu quả của giải pháp | 07/08/2026 | 07/08/2026 | <https://aws.amazon.com/cloudwatch/> |

### Kết quả đạt được tuần 7:

* Tiến hành thành công các thử nghiệm failover để đánh giá khả năng chịu lỗi của hệ thống.
* Giả lập sự cố trên một EC2 instance và quan sát hệ thống chuyển hướng traffic qua ALB đến instance còn hoạt động.
* Xác nhận Auto Scaling Group có thể tự động thay thế instance bị lỗi hoặc mở thêm instance mới khi cần thiết.
* Đánh giá được thời gian phục hồi của hệ thống trong các tình huống mất một node hoặc dịch vụ bị gián đoạn.
* Kiểm tra hiệu quả của health check trong việc phát hiện instance không healthy và loại bỏ khỏi target group.
* Nhận thấy hệ thống giữ được khả năng hoạt động trong hầu hết các kịch bản failover đã thử nghiệm.
* Thu thập dữ liệu về độ trễ, độ sẵn sàng và mức độ ổn định của ứng dụng trước và sau khi xảy ra sự cố.

### Bài học rút ra:

* Failover testing là bước quan trọng để xác nhận rằng hệ thống thực sự có khả năng chịu lỗi, không chỉ ở lý thuyết mà còn ở thực tế.
* Load Balancer và Auto Scaling đóng vai trò then chốt trong việc giảm thiểu thời gian gián đoạn khi có instance bị lỗi.
* Health check là cơ chế quan trọng giúp hệ thống nhận diện instance không hoạt động và ngăn không cho traffic được chuyển tới node đó.
* Một hệ thống High Availability hiệu quả không cần tránh hoàn toàn sự cố, mà cần giảm thiểu thời gian ngừng hoạt động và đảm bảo dịch vụ tiếp tục phục vụ người dùng.
* Kết quả kiểm thử cho thấy việc thiết kế kiến trúc phân tán và dự phòng là yếu tố quyết định đến tính sẵn sàng của hệ thống.

### Đánh giá chung:

Tuần 7 là giai đoạn đánh giá thực tế hiệu quả của giải pháp AWS mà tôi đã triển khai. Thông qua việc giả lập sự cố và tiến hành failover, tôi đã thấy rõ sự đóng góp của ALB, Auto Scaling và CloudWatch trong việc nâng cao độ ổn định và tính sẵn sàng của hệ thống. Kết quả kiểm thử không chỉ cho thấy hệ thống có khả năng phục hồi sau lỗi mà còn giúp tôi nhận diện các điểm cần cải thiện để tiếp tục tối ưu hóa trong tương lai.

