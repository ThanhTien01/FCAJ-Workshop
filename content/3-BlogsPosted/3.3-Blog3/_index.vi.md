---
title: "Blog 3"
date: 2024-01-01
weight: 1
chapter: false
pre: " <b> 3.3. </b> "
---

# Tự động hóa quản lý ngân sách trên Multi-Account Environments

Khi sử dụng AWS trong môi trường có nhiều tài khoản, việc theo dõi và kiểm soát chi phí trở nên khó khăn hơn. Mỗi account có thể được sử dụng cho một mục đích khác nhau như Development, Testing hoặc Production, dẫn đến chi phí phát sinh ở nhiều nơi.

Nếu quản lý ngân sách thủ công cho từng account, việc thiết lập và theo dõi sẽ mất nhiều thời gian. Vì vậy, AWS cung cấp các dịch vụ và cơ chế tự động hóa giúp quản lý Budget hiệu quả trên môi trường Multi-Account.

### Multi-Account Environment là gì?

Trong AWS, doanh nghiệp có thể sử dụng nhiều AWS Account để phân tách môi trường và workload.

Ví dụ:

- Account Development: dành cho quá trình phát triển và thử nghiệm.
- Account Staging: dành cho kiểm thử trước khi triển khai.
- Account Production: chạy ứng dụng thực tế.
- Account Security hoặc Logging: quản lý các chức năng dùng chung.

>Việc phân chia account giúp tăng tính bảo mật, dễ quản lý quyền truy cập và dễ kiểm soát chi phí. Tuy nhiên, số lượng account càng nhiều thì việc quản lý ngân sách càng trở nên phức tạp.

### Vấn đề khi quản lý Budget thủ công

Nếu mỗi AWS Account được thiết lập Budget riêng bằng cách thủ công, người quản trị cần thực hiện nhiều thao tác lặp lại.

Một số vấn đề thường gặp:

- Mất nhiều thời gian khi tạo Budget cho nhiều account.
- Dễ cấu hình sai hoặc bỏ sót account mới.
- Khó duy trì cùng một chính sách ngân sách.
- Khó theo dõi khi số lượng account tăng lên.
- Phải kiểm tra thủ công khi chi phí vượt mức cho phép.

>Do đó, tự động hóa Budget sẽ giúp giảm đáng kể công việc quản trị.

### Automating Budget Management

Ý tưởng chính là xây dựng một quy trình có thể tự động tạo và quản lý Budget cho các AWS Account.

Thay vì đăng nhập vào từng account để thiết lập Budget, chúng ta có thể sử dụng một account trung tâm để quản lý và triển khai cấu hình Budget cho các account thành viên.

Quy trình có thể được thực hiện theo các bước:

#### 1. Xác định ngân sách cho từng account

Trước tiên, cần xác định mức ngân sách phù hợp cho từng account.

Ví dụ:

- Development: 100 USD/tháng.
- Staging: 200 USD/tháng.
- Production: 1.000 USD/tháng.

>Các mức ngân sách có thể được lưu trong một cấu hình chung để dễ dàng thay đổi và quản lý.

#### 2. Tự động tạo AWS Budget
AWS Budgets có thể được sử dụng để theo dõi chi phí và thiết lập các ngưỡng cảnh báo.

Ví dụ, có thể thiết lập cảnh báo khi chi phí đạt:

- 50% ngân sách.
- 80% ngân sách.
- 100% ngân sách.

>Khi đạt ngưỡng, hệ thống có thể gửi thông báo để người quản trị biết và kiểm tra nguyên nhân tăng chi phí.

#### 3. Áp dụng cho nhiều Account

Trong môi trường AWS Organizations, các account được quản lý tập trung từ một Management Account hoặc một account quản trị chuyên dụng.

Việc kết hợp AWS Organizations với cơ chế tự động hóa giúp triển khai chính sách Budget đồng nhất cho nhiều account.

Khi có một account mới được tạo, hệ thống có thể tự động thiết lập Budget theo cấu hình đã định trước thay vì phải thực hiện thủ công.

#### 4. Gửi cảnh báo chi phí 
Một phần quan trọng của việc quản lý Budget là thông báo khi chi phí vượt mức.

Có thể sử dụng Amazon SNS để gửi cảnh báo đến email hoặc các hệ thống thông báo khác.

Ví dụ:

>Development Account đã sử dụng 80% ngân sách tháng này.

Nhờ đó, nhóm phát triển có thể kiểm tra các tài nguyên đang chạy và thực hiện tối ưu nếu cần.

### Lợi ích của việc tự động hóa

Automating Budget Management mang lại một số lợi ích đáng chú ý:

*Tiết kiệm thời gian:* 
Không cần thiết lập Budget thủ công cho từng account.

*Giảm sai sót:*
Các account có thể sử dụng cùng một quy tắc và cấu hình Budget.

*Dễ mở rộng:*
Khi số lượng AWS Account tăng lên, hệ thống vẫn có thể quản lý Budget một cách tự động.

*Kiểm soát chi phí tốt hơn:*
Các cảnh báo giúp phát hiện sớm tình trạng chi phí tăng bất thường.

*Quản lý tập trung:*
Người quản trị có thể xây dựng chính sách quản lý chi phí thống nhất cho toàn bộ AWS Organization.

### Kết luận 
**Automating Budget Management Across Multi-Account Environments** là một giải pháp hữu ích khi hệ thống AWS có nhiều account và workload khác nhau.

Thay vì quản lý ngân sách thủ công, việc kết hợp AWS Organizations, AWS Budgets và các dịch vụ thông báo giúp tự động hóa quá trình theo dõi và cảnh báo chi phí.

Đối với môi trường AWS ngày càng mở rộng, tự động hóa Budget không chỉ giúp tiết kiệm thời gian quản trị mà còn góp phần xây dựng một quy trình Cost Management chủ động, nhất quán và dễ mở rộng.