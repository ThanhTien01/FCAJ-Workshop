---
title: "Blog 2"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.2. </b> "
---

# Tối ưu thời gian Docker Build trên AWS CodeBuild bằng Amazon ECR

Docker được sử dụng phổ biến để đóng gói và triển khai ứng dụng. Trong các quy trình CI/CD, việc build Docker image được thực hiện nhiều lần, vì vậy thời gian build có thể ảnh hưởng trực tiếp đến tốc độ triển khai.

AWS CodeBuild hỗ trợ tự động hóa quá trình build ứng dụng, trong khi Amazon ECR được sử dụng để lưu trữ Docker image. Tuy nhiên, nếu không tận dụng Docker cache, nhiều bước trong quá trình build có thể phải thực hiện lại, gây tốn thời gian.

Trong bài viết này, chúng ta sẽ tìm hiểu cách sử dụng Amazon ECR làm remote cache để Docker có thể sử dụng lại các layer đã được build trước đó, từ đó giúp giảm thời gian build Docker image trên AWS CodeBuild.

#### 1. Docker Cache là gì?
Docker image được tạo từ nhiều layer. Khi một layer không thay đổi, Docker có thể sử dụng lại layer đó thay vì build lại.

Ví dụ, nếu ứng dụng chỉ thay đổi source code nhưng các thư viện không thay đổi, Docker có thể sử dụng lại phần đã cài đặt thư viện.

Điều này giúp giảm thời gian build Docker image.

#### 2. Vấn đề khi sử dụng CodeBuild
AWS CodeBuild cung cấp môi trường để tự động build ứng dụng. Tuy nhiên, Docker cache không phải lúc nào cũng được giữ lại giữa các lần build.

Khi không có cache, Docker phải thực hiện lại nhiều bước từ đầu. Điều này làm thời gian build tăng lên, đặc biệt đối với những project có nhiều thư viện.

#### 3. Sử dụng Amazon ECR làm Remote Cache
Amazon ECR thường được sử dụng để lưu trữ Docker image.

Trong trường hợp này, ECR còn được sử dụng để lưu Docker cache. Cache được lưu trên ECR có thể được sử dụng lại trong những lần build tiếp theo.

Quá trình hoạt động khá đơn giản:

- CodeBuild bắt đầu build Docker image.
- Docker kiểm tra cache trên ECR.
- Những phần không thay đổi được sử dụng lại.
- Những phần thay đổi sẽ được build lại.
- Cache mới được lưu lại trên ECR.

Nhờ vậy, Docker không cần build lại toàn bộ image trong mỗi lần chạy.

#### 4. Một số cách tối ưu 
Để sử dụng cache hiệu quả hơn, cần viết Dockerfile hợp lý.

Các phần ít thay đổi nên được xử lý trước, còn source code thường xuyên thay đổi nên để sau.

Ngoài ra, có thể sử dụng **.dockerignore** để bỏ qua những file không cần thiết như **.git**, **node_modules** hoặc các file build cũ.

Những cách này giúp giảm thời gian và tài nguyên trong quá trình Docker build.

#### 5. Lợi ích
Việc sử dụng Amazon ECR làm remote cache giúp:

- Giảm thời gian build Docker image.
- Tận dụng lại các layer đã có.
- Giảm việc build lại những phần không thay đổi.
- Cải thiện tốc độ của pipeline CI/CD.
- Kết hợp hiệu quả giữa CodeBuild và ECR.

### Kết luận 

Tối ưu thời gian Docker Build là một bước quan trọng để cải thiện hiệu quả của quy trình CI/CD. Việc sử dụng Amazon ECR làm remote cache giúp Docker tận dụng lại các layer đã được build trước đó, từ đó hạn chế việc phải build lại toàn bộ image trong mỗi lần triển khai.

Kết hợp Docker, AWS CodeBuild và Amazon ECR không chỉ giúp rút ngắn thời gian build mà còn tạo ra một quy trình build ổn định và hiệu quả hơn. Bên cạnh đó, việc tối ưu Dockerfile và sử dụng cache hợp lý cũng đóng vai trò quan trọng trong việc cải thiện hiệu suất.

Đây là một giải pháp đơn giản nhưng hữu ích đối với các dự án sử dụng Docker và AWS, đặc biệt khi ứng dụng được build và triển khai thường xuyên.