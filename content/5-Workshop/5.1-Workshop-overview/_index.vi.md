---
title : "Giới thiệu"
date : 2024-01-01 
weight : 1 
chapter : false
pre : " <b> 5.1. </b> "
---

Điện toán đám mây đã trở thành nền tảng quan trọng đối với các hệ thống công nghệ thông tin hiện đại. Khi các ứng dụng web phục vụ lượng người dùng ngày càng tăng, việc đảm bảo tính sẵn sàng, độ tin cậy và khả năng đáp ứng linh hoạt trước sự thay đổi của tải hệ thống trở thành yêu cầu thiết yếu. Một ứng dụng web chỉ triển khai trên một máy chủ đơn lẻ có thể rơi vào trạng thái ngưng hoạt động khi máy chủ gặp sự cố phần cứng, trục trặc mạng hoặc lưu lượng truy cập tăng đột biến. Điều này tạo ra **Điểm lỗi đơn lẻ (Single Point of Failure - SPOF)** và dẫn đến gián đoạn dịch vụ.

![Multi-AZ High Availability Architecture](/images/5-Workshop/5.1-Workshop-overview/multi-az-architecture.png)

**Tính sẵn sàng cao (High Availability - HA)** là giải pháp giúp giảm thiểu tối đa thời gian ngừng hoạt động của dịch vụ bằng cách phân bổ tài nguyên ứng dụng trên nhiều thành phần hạ tầng độc lập. Trên AWS, kiến trúc tính sẵn sàng cao được thiết lập bằng cách kết hợp nhiều **Availability Zones (AZs)** cùng với các dịch vụ cốt lõi như **Amazon EC2, Amazon RDS, Application Load Balancer, Auto Scaling, Amazon S3 và Amazon CloudWatch**. Các dịch vụ này cung cấp những năng lực đa dạng về tính toán, quản trị cơ sở dữ liệu, phân phối lưu lượng truy cập, tự động co giãn tài nguyên, lưu trữ, giám sát và khôi phục hệ thống.

Trong bài workshop này, một **ứng dụng web bằng Python** sẽ được triển khai trên AWS và thiết kế để vận hành trải dài trên nhiều Availability Zones khác nhau. **Application Load Balancer (ALB)** được sử dụng để phân phối các yêu cầu đi vào đến các máy chủ ứng dụng đang hoạt động ổn định, trong khi **Auto Scaling Group (ASG)** tự động điều chỉnh số lượng máy chủ EC2 linh hoạt theo tải của hệ thống. Amazon RDS được dùng làm dịch vụ cơ sở dữ liệu quản trị, còn Amazon S3 đóng vai trò lưu trữ đối tượng trên đám mây. Bên cạnh đó, Amazon CloudWatch cũng được cấu hình để giám sát hiệu năng và các hoạt động vận hành của toàn bộ hệ thống.

![Single Point of Failure Architecture](/images/5-Workshop/5.1-Workshop-overview/spof-architecture.png)

Bài workshop không chỉ tập trung vào việc triển khai ứng dụng mà còn đi sâu vào **kiểm thử tính sẵn sàng và khả năng chịu lỗi (fault tolerance) của hệ thống**. Các kịch bản chuyển vùng thất bại (failover) được thực hiện bằng cách giả lập sự cố ngắt kết nối trên một máy chủ ứng dụng và quan sát cách Load Balancer cùng Auto Scaling Group phản ứng. Kết quả sau đó được đánh giá để xác định liệu hệ thống có duy trì được tính liên tục của dịch vụ và tự động khôi phục khi xảy ra lỗi trên từng tài nguyên đơn lẻ hay không.

Toàn bộ quá trình thực hiện bám sát theo kế hoạch thực tập kéo dài 8 tuần, bao gồm các bước: tìm hiểu khái niệm High Availability, thiết kế kiến trúc Multi-AZ, triển khai ứng dụng, cấu hình các dịch vụ AWS, thiết lập Load Balancing & Auto Scaling, cài đặt hệ thống giám sát & nhật ký (logging), thực hiện kiểm thử failover và đánh giá tổng thể hệ thống cuối cùng.