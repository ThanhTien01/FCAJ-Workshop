---
title: "Worklog Tuần 6"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.6. </b> "
---

### Mục tiêu tuần 6:

* Thiết lập hệ thống giám sát và ghi nhật ký cho ứng dụng trên AWS.
* Tìm hiểu cách Amazon CloudWatch thu thập metrics và logs từ EC2, ALB và các dịch vụ liên quan.
* Tạo alarm và cảnh báo nhằm phản ứng nhanh trước các sự cố hoặc mức tải bất thường.
* Nâng cao khả năng quản trị hệ thống bằng mô hình monitoring và logging tập trung.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Tìm hiểu vai trò của CloudWatch trong giám sát hệ thống AWS <br> - Nghiên cứu các loại metric, log và alarm | 27/07/2026 | 27/07/2026 | <https://aws.amazon.com/cloudwatch/> |
| 3 | - Cấu hình CloudWatch trên EC2 <br> - Bật các metrics cơ bản như CPU, memory, disk và network | 28/07/2026 | 28/07/2026 | <https://aws.amazon.com/cloudwatch/> |
| 4 | - Thiết lập log group và gửi log từ ứng dụng Python lên CloudWatch Logs <br> - Kiểm tra định dạng log và cấu trúc nhật ký | 29/07/2026 | 29/07/2026 | <https://aws.amazon.com/cloudwatch/> |
| 5 | - Tạo alarm cảnh báo cho CPU, trạng thái instance và lỗi hệ thống <br> - Thiểm tra alert khi tiêu thụ tài nguyên tăng cao | 30/07/2026 | 30/07/2026 | <https://aws.amazon.com/cloudwatch/> |
| 6 | - Tổng hợp dữ liệu giám sát, đánh giá hiệu quả monitoring <br> - Ghi nhận bài học và đề xuất cải tiến cho hệ thống | 31/07/2026 | 31/07/2026 | <https://aws.amazon.com/cloudwatch/> |

### Kết quả đạt được tuần 6:

* Hiểu rõ vai trò của CloudWatch trong việc giám sát, theo dõi và cảnh báo các vấn đề của hệ thống AWS.
* Thiết lập thành công các metric cơ bản trên EC2 như CPU utilization, disk usage và network traffic.
* Cấu hình log từ ứng dụng Python và gửi lên CloudWatch Logs để lưu trữ và phân tích nhật ký theo thời gian thực.
* Nắm được cách quản lý log group, stream log và truy vấn dữ liệu nhật ký khi sự cố xảy ra.
* Tạo alarm cảnh báo cho các tình huống như CPU quá tải, khe hở tài nguyên hoặc lỗi hoạt động hệ thống.
* Kiểm tra thành công khả năng phản ứng của alarm khi hệ thống gặp tải cao hoặc trạng thái bất thường.
* Có khả năng phân tích nguyên nhân sự cố thông qua metric và log, giúp thời gian debug giảm đáng kể.
* Nhận thấy tầm quan trọng của monitoring và logging trong việc duy trì độ ổn định và tính sẵn sàng của hệ thống.

### Bài học rút ra:

* Monitoring không chỉ giúp quan sát trạng thái hệ thống mà còn là công cụ hỗ trợ quyết định trong quá trình vận hành và tối ưu hóa tài nguyên.
* CloudWatch cung cấp cái nhìn tổng quan về hoạt động của EC2, ALB và các dịch vụ liên quan, giúp phát hiện sớm nguy cơ hệ thống gặp sự cố.
* Logs là nguồn dữ liệu quan trọng để tìm hiểu nguyên nhân sự cố, trong khi metrics giúp đánh giá xu hướng tăng giảm của tải hệ thống.
* Alarm là phần quan trọng để giảm thời gian phản ứng khi có vấn đề, đặc biệt trong môi trường production.
* Một hệ thống tốt không chỉ chạy ổn định mà còn cần có cơ chế giám sát rõ ràng để người vận hành có thể chủ động xử lý ngay khi có dấu hiệu bất thường.

### Đánh giá chung:

Tuần 6 là giai đoạn tôi tập trung vào khía cạnh vận hành hệ thống, khi ứng dụng đã được triển khai và chạy trên môi trường AWS. Việc thiết lập monitoring và logging với CloudWatch giúp tôi hiểu rõ hơn về cách theo dõi hiệu suất, phát hiện lỗi và phản ứng nhanh trước các sự cố. Đây là bước quan trọng để chuyển từ triển khai cơ bản sang vận hành hệ thống thực tế, đồng thời tạo nền tảng cho các đánh giá và cải tiến trong các tuần tiếp theo.

