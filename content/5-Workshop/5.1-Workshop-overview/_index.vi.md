---
title : "Giới thiệu"
date : 2024-01-01 
weight : 1 
chapter : false
pre : " <b> 5.1. </b> "
---

Điện toán đám mây đã trở thành nền tảng quan trọng cho các hệ thống công nghệ thông tin hiện đại. Khi các ứng dụng web phục vụ ngày càng nhiều người dùng, đảm bảo tính sẵn sàng của hệ thống, độ tin cậy và khả năng phản hồi với khối lượng công việc thay đổi đã trở thành một yêu cầu quan trọng. Một ứng dụng web triển khai trên một máy chủ duy nhất có thể bị gián đoạn khi máy chủ gặp sự cố phần cứng, sự cố mạng hoặc lưu lượng truy cập tăng đột ngột. Điều này tạo ra một **Single Point of Failure - (SPOF)** và có thể dẫn đến việc ngừng dịch vụ.

![Kiến trúc sẵn sàng cao Multi-AZ](/images/5-Workshop/5.1-Workshop-overview/aws-architecture.png)

**High Availability** là một phương pháp được sử dụng để giảm thiểu thời gian gián đoạn dịch vụ bằng cách phân phối tài nguyên ứng dụng qua nhiều thành phần hạ tầng độc lập. Trên AWS, sẵn sàng cao có thể đạt được bằng cách kết hợp nhiều **Availability Zones** với các dịch vụ như **Amazon EC2, Amazon RDS, Application Load Balancer, Auto Scaling, Amazon S3 và Amazon CloudWatch**. Các dịch vụ này cung cấp các khả năng khác nhau về tính toán, quản lý cơ sở dữ liệu, phân phối lưu lượng, tự động điều chỉnh tài nguyên, lưu trữ, giám sát và khôi phục hệ thống.

Trong workshop này, một **ứng dụng web viết bằng Python** được triển khai trên AWS và thiết kế để hoạt động trên nhiều Vùng khả dụng. Một **Application Load Balancer (ALB)** được sử dụng để phân phối các yêu cầu đến các máy chủ ứng dụng khỏe mạnh, trong khi một **Auto Scaling Group (ASG)** tự động điều chỉnh số lượng phiên bản EC2 theo khối lượng công việc của hệ thống. Amazon RDS được sử dụng để cung cấp dịch vụ cơ sở dữ liệu được quản lý, còn Amazon S3 cung cấp lưu trữ đối tượng trên đám mây. Amazon CloudWatch cũng được cấu hình để giám sát hiệu suất hệ thống và hoạt động vận hành.

![Kiến trúc điểm hỏng duy nhất](/images/5-Workshop/5.1-Workshop-overview/spof.png)

Workshop này tập trung không chỉ vào việc triển khai ứng dụng mà còn vào **kiểm thử tính sẵn sàng và khả năng chịu lỗi của hệ thống**. Các kịch bản chuyển đổi dự phòng được thực hiện bằng cách mô phỏng sự cố của một phiên bản ứng dụng và quan sát cách Load Balancer cùng Auto Scaling Group phản ứng. Kết quả sau đó được đánh giá để xác định hệ thống có thể duy trì tính sẵn sàng dịch vụ và tự động khôi phục khi xảy ra lỗi ở từng tài nguyên hay không.

Việc triển khai tổng thể theo đúng lộ trình thực tập tám tuần đã lên kế hoạch, bao gồm nghiên cứu các khái niệm về Sẵn sàng cao, thiết kế kiến trúc Multi-AZ, triển khai ứng dụng, cấu hình các dịch vụ AWS, thực hiện Load Balancing và Auto Scaling, thiết lập giám sát và ghi nhật ký, thực hiện kiểm thử chuyển đổi dự phòng và đánh giá hệ thống cuối cùng.