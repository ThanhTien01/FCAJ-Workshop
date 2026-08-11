---
title: "Worklog Tuần 4"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.4. </b> "
---


### Mục tiêu tuần 4:

* Triển khai thành phần nền tảng hệ thống lên môi trường AWS.
* Thiết lập EC2 để chạy ứng dụng backend và triển khai service chính.
* Tạo và cấu hình Amazon RDS để lưu trữ dữ liệu quan trọng của hệ thống.
* Sử dụng Amazon S3 để lưu trữ dữ liệu tĩnh và các file cần thiết.
* Kiểm tra kết nối giữa các thành phần và đảm bảo hệ thống hoạt động ổn định.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Xác định cấu hình EC2 phù hợp cho ứng dụng Python <br> - Lựa chọn AMI, instance type và storage cần thiết | 13/07/2026 | 13/07/2026 | <https://aws.amazon.com/ec2/> |
| 3 | - Tạo EC2 instance trên AWS <br> - Cấu hình security group, key pair và SSH access <br> - Kết nối vào instance từ máy local | 14/07/2026 | 14/07/2026 | <https://aws.amazon.com/ec2/> |
| 4 | - Cài đặt môi trường chạy ứng dụng trên EC2 <br> - Cài đặt Python, dependency và cấu hình server | 15/07/2026 | 15/07/2026 | <https://aws.amazon.com/ec2/> |
| 5 | - Tạo Amazon RDS instance <br> - Thiết lập database, parameter group và kết nối từ ứng dụng EC2 | 16/07/2026 | 16/07/2026 | <https://aws.amazon.com/rds/> |
| 6 | - Tạo S3 bucket và cấu hình quyền truy cập <br> - Kiểm tra toàn bộ luồng dữ liệu từ EC2 tới RDS và S3 <br> - Ghi nhận lỗi và tối ưu cấu hình | 17/07/2026 | 17/07/2026 | <https://aws.amazon.com/s3/> |

### Kết quả đạt được tuần 4:

* Thành công trong việc triển khai EC2 instance trên AWS để làm nền tảng chạy ứng dụng.
* Thiết lập thành công key pair, security group và kết nối SSH để quản lý instance từ máy local.
* Cài đặt môi trường Python trên EC2 và đảm bảo ứng dụng demo có thể chạy trên server cloud.
* Tạo và cấu hình Amazon RDS để lưu trữ dữ liệu hệ thống, đồng thời kiểm tra khả năng kết nối từ ứng dụng phía EC2.
* Sử dụng Amazon S3 để lưu trữ dữ liệu tĩnh, file tải lên và các tài nguyên phụ trợ của hệ thống.
* Nắm được cách tương tác giữa các thành phần chính trong kiến trúc AWS: EC2 - RDS - S3.
* Kiểm tra được luồng dữ liệu và xác nhận các thiết lập cơ bản về kết nối, bảo mật và quyền truy cập đã hoạt động đúng.
* Phát hiện và khắc phục một số lỗi trong quá trình triển khai như sai cấu hình port, thiếu IAM permission hoặc lỗi kết nối database.

### Bài học rút ra:

* Việc triển khai ứng dụng lên AWS không chỉ là tạo instance mà còn cần cấu hình mạng, nhóm bảo mật và quyền truy cập đúng cách để tránh lỗi về kết nối.
* EC2 là thành phần quan trọng để chạy ứng dụng, nhưng để hệ thống vận hành ổn định cần có một cơ sở dữ liệu tương ứng như RDS và lưu trữ dữ liệu tĩnh như S3.
* RDS giúp giảm tải cho ứng dụng trong việc quản lý dữ liệu và đảm bảo tính bền vững cho dữ liệu quan trọng.
* S3 là giải pháp hiệu quả để lưu trữ file, hình ảnh, backup hoặc dữ liệu phục vụ truy xuất nhanh.
* Trong quá trình triển khai, việc kiểm tra kỹ từng bước ngay từ SSH, security group, database connection string đến permissions sẽ giúp giảm thiểu rủi ro và thời gian debug.

### Đánh giá chung:

Tuần 4 là giai đoạn chuyển từ phát triển local sang triển khai hệ thống trên môi trường cloud. Với việc triển khai EC2, RDS và S3, tôi đã có cái nhìn rõ hơn về cách mà các thành phần trong hệ thống AWS phối hợp với nhau để tạo ra một ứng dụng thực tế có thể vận hành ổn định. Đây là nền tảng quan trọng để bước sang các tuần tiếp theo, khi hệ thống sẽ được mở rộng và tối ưu hóa hơn với các thành phần nâng cao như Load Balancer, Auto Scaling và Monitoring.

