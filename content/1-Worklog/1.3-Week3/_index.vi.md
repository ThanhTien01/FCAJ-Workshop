---
title: "Worklog Tuần 3"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 1.3. </b> "
---


### Mục tiêu tuần 3:

* Cài đặt và chuẩn hóa môi trường phát triển cho dự án.
* Tìm hiểu các công cụ cần thiết để xây dựng ứng dụng Python.
* Xây dựng một ứng dụng demo đơn giản để kiểm tra khả năng triển khai và vận hành.
* Nắm được quy trình chạy ứng dụng local trước khi triển khai lên môi trường AWS.

### Các công việc cần triển khai trong tuần này:

| Thứ | Công việc | Ngày bắt đầu | Ngày hoàn thành | Nguồn tài liệu |
| --- | --- | --- | --- | --- |
| 2 | - Làm quen với môi trường làm việc và định hướng dự án <br> - Xác định yêu cầu cơ bản cho ứng dụng demo Python | 06/07/2026 | 06/07/2026 |  |
| 3 | - Cài đặt Python, pip và các công cụ hỗ trợ phát triển <br> - Kiểm tra phiên bản và cấu hình hệ thống <br> - Tạo môi trường ảo (virtual environment) | 07/07/2026 | 07/07/2026 | <https://www.python.org/> |
| 4 | - Cài đặt thư viện cần thiết cho ứng dụng demo: Flask/FastAPI, requests, dotenv <br> - Tìm hiểu kiến trúc cơ bản của ứng dụng web Python | 08/07/2026 | 08/07/2026 | <https://flask.palletsprojects.com/> |
| 5 | - Xây dựng ứng dụng demo đầu tiên <br> - Tạo route, xử lý request và hiển thị dữ liệu mẫu <br> - Kiểm tra tính hoạt động cục bộ | 09/07/2026 | 10/07/2026 | <https://fastapi.tiangolo.com/> |
| 6 | - Hoàn thiện giao diện demo, kiểm thử chức năng và ghi nhận kết quả <br> - Chuẩn bị tài liệu và học tập từ các lỗi phát sinh trong quá trình chạy | 10/07/2026 | 10/07/2026 |  |

### Kết quả đạt được tuần 3:

* Hoàn tất việc cài đặt môi trường phát triển Python trên máy tính cá nhân, bao gồm:
  * Python phiên bản phù hợp
  * pip để quản lý dependency
  * virtual environment để tách môi trường làm việc
  * các công cụ hỗ trợ phát triển cơ bản

* Hiểu rõ vai trò của môi trường ảo trong việc quản lý phiên bản package và tránh xung đột giữa các dự án.

* Tạo được ứng dụng demo bằng Python với mô hình backend đơn giản, có khả năng xử lý HTTP request và trả về dữ liệu dưới dạng JSON hoặc giao diện web cơ bản.

* Thành công trong việc thiết lập cấu trúc dự án cơ bản như:
  * thư mục source code
  * file cấu hình
  * file khởi chạy ứng dụng
  * các route xử lý API đơn giản

* Thực hiện kiểm thử ứng dụng local bằng cách chạy server và truy cập vào các endpoint đã tạo.

* Nắm được cách hoạt động của một ứng dụng web đơn giản trong Python, từ nhận request, xử lý logic, đến trả phản hồi cho client.

* Học được cách debug các lỗi phát sinh trong quá trình cài đặt package, khởi động ứng dụng và chạy thử chức năng.

* Xây dựng nền tảng ban đầu cho các công việc triển khai AWS sau này, khi ứng dụng demo sẽ được chạy trên EC2, container hoặc môi trường cloud khác.

### Bài học rút ra:

* Việc cài đặt môi trường phát triển đúng cách là bước đầu tiên và rất quan trọng trong mọi dự án kỹ thuật. Nếu môi trường không được chuẩn hóa, các lỗi về package, phiên bản hoặc cấu hình sẽ làm chậm tiến độ rất nhiều.
* Python là ngôn ngữ phù hợp để xây dựng ứng dụng demo nhanh nhờ cú pháp đơn giản và hệ sinh thái thư viện phong phú.
* Một ứng dụng demo dù nhỏ nhưng phải có cấu trúc rõ ràng để dễ mở rộng trong tương lai.
* Quá trình chạy thử cục bộ giúp phát hiện lỗi sớm hơn, đặc biệt là lỗi liên quan đến dependency, import module và định tuyến ứng dụng.
* Việc xây dựng ứng dụng demo trước khi deploy lên AWS giúp tôi hiểu rõ vòng đời phát triển phần mềm, từ local environment đến triển khai production.

### Đánh giá chung:

Tuần 3 đã giúp tôi xây dựng nền tảng rất quan trọng cho dự án: từ môi trường làm việc, cách quản lý package, đến việc phát triển một ứng dụng Python demo đầu tiên. Đây là bước khởi đầu cần thiết để sau này triển khai ứng dụng lên AWS, tích hợp các dịch vụ cloud và xây dựng hệ thống theo mô hình High Availability. Kết quả đạt được trong tuần này không chỉ giúp tôi hiểu sâu hơn về lập trình Python mà còn tạo tiền đề cho các giai đoạn thực hành tiếp theo trên môi trường thực tế.

