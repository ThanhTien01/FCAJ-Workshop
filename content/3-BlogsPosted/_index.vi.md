---
title: "Các bài blogs đã đăng"
date: 2024-01-01
weight: 3
chapter: false
pre: " <b> 3. </b> "
---

Trong quá trình thực tập, tôi đã thực hiện và đăng 03 bài blog lên cộng đồng [AWS Study Group](https://www.facebook.com/groups/awsstudygroupfcj). Các bài viết tập trung vào việc chia sẻ kiến thức, kinh nghiệm tìm hiểu và áp dụng các dịch vụ, giải pháp AWS trong quá trình thực tập.

###  [Blog 1 - Các phương pháp hay nhất về kích thước phù hợp cho Amazon EC2](3.1-Blog1/)
Blog giới thiệu về Right Sizing Amazon EC2, một phương pháp giúp lựa chọn cấu hình EC2 phù hợp với nhu cầu thực tế. Nội dung tập trung vào các phương pháp tối ưu như kiểm tra và đo lường tài nguyên, lựa chọn instance phù hợp, nhóm các workload tương tự và kết hợp Savings Plans/Reserved Instances để tối ưu chi phí AWS.

###  [Blog 2 - Tối ưu thời gian Docker Build trên AWS CodeBuild bằng Amazon ECR](3.2-Blog2/)
Blog này giới thiệu cách tối ưu thời gian build Docker image trên AWS CodeBuild bằng Amazon ECR làm remote cache.
Trong quá trình build Docker image, một số bước có thể mất nhiều thời gian nếu phải thực hiện lại trong mỗi lần build. Việc sử dụng remote cache cho phép Docker tận dụng lại các layer đã được build trước đó, giúp giảm thời gian build và tăng hiệu quả của quy trình CI/CD.
Bài viết sẽ trình bày cách Docker, AWS CodeBuild và Amazon ECR kết hợp với nhau để tối ưu quá trình build Docker image một cách đơn giản và hiệu quả.

###  [Blog 3 - Tự động hóa quản lý ngân sách trên Multi-Account Environments](3.3-Blog3/)
Blog này giới thiệu cách tự động hóa việc quản lý ngân sách trên môi trường AWS Multi-Account. Khi số lượng AWS Account tăng lên, việc theo dõi và kiểm soát chi phí thủ công sẽ trở nên khó khăn và tốn nhiều thời gian.
Bài viết sẽ trình bày cách sử dụng AWS Budgets kết hợp với AWS Organizations để thiết lập ngân sách, theo dõi chi phí và gửi cảnh báo tự động cho nhiều AWS Account. Qua đó, giúp doanh nghiệp kiểm soát chi phí hiệu quả hơn và giảm công việc quản trị thủ công.