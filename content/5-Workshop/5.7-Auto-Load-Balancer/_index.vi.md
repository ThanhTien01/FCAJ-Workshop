---
title: "Cấu hình Application Load Balancer"
date: 2024-01-01
weight: 7
chapter: false
pre: " <b> 5.7. </b> "
---

### 1. Tạo Target Group (Khởi tạo Target Group)

Để **Application Load Balancer (ALB)** có thể định tuyến lưu lượng truy cập (traffic) từ người dùng đến ứng dụng, trước tiên chúng ta cần tạo một **Target Group**. Target Group đóng vai trò gom nhóm các tài nguyên máy chủ backend (như các EC2 instances) và liên tục kiểm tra trạng thái hoạt động (**Health Check**) của chúng.

---

#### Bảng thông số cấu hình Target Group

| Trường thông số | Giá trị cấu hình | Giải thích |
| :--- | :--- | :--- |
| **Target type** | `Instances` | Định tuyến trực tiếp đến các máy chủ EC2 |
| **Target group name** | `fca-web-target-group` | Tên nhận diện của Target Group |
| **Protocol** | `HTTP` | Giao thức truyền tải web |
| **Port** | `5000` | Cổng dịch vụ ứng dụng Flask đang lắng nghe |
| **IP address type** | `IPv4` | Chuẩn địa chỉ IP |
| **VPC** | `fca-workshop-vpc` | VPC chứa hạ tầng ứng dụng |
| **Health check path** | `/` | Đường dẫn URL để ALB kiểm tra độ sẵn sàng |

> **Lưu ý về Cổng (Port 5000):** Vì ứng dụng Python Flask trên EC2 đang chạy và lắng nghe ở cổng `5000` (`0.0.0.0:5000`), ALB cần gửi các yêu cầu đến chính xác cổng này trên EC2.

---

#### Các bước thực hiện trên AWS Console

##### Bước 1: Mở giao diện Target Groups
1. Truy cập **AWS Management Console** → dịch vụ **EC2**.
2. Tại menu bên trái, cuộn xuống mục **Load Balancing** → chọn **Target Groups**.
3. Bấm nút màu cam **Create target group**.

##### Bước 2: Chọn Target Type & Thiết lập thông số
1. Tại phần **Choose a target type**, tích chọn **Instances**.
2. Nhập các thông số chi tiết:
   * **Target group name:** `fca-web-target-group`
   * **Protocol:** `HTTP`
   * **Port:** `5000`
   * **VPC:** Chọn VPC riêng `fca-workshop-vpc`

##### Bước 3: Cấu hình Health Checks
1. Tại phần **Health checks**:
   * **Health check protocol:** `HTTP`
   * **Health check path:** `/`
2. Các thông số *Advanced health check settings* khác giữ nguyên mặc định.
3. Nhấp chọn **Next** ở cuối trang.

##### Bước 4: Hoàn tất tạo Target Group
1. Tại màn hình **Register targets**, tạm thời **chưa chọn/register EC2 instance** ở bước này (chúng ta sẽ register ở bước 5.7.4).
2. Cuộn xuống cuối trang và nhấp chọn **Create target group**.

<p align="center">
  <img src="/images/5-Workshop/5.7-ALB/target-group-created.png" alt="Target Group Created" width="85%" />
  <br>
  <em>Figure 5.13: Target Group Created Successfully</em>
</p>

---

### 2. Cấu hình Application Load Balancer (ALB)

**Application Load Balancer (ALB)** đóng vai trò là điểm tiếp nhận lưu lượng truy cập duy nhất từ Internet (Entry Point), sau đó tự động phân phối các yêu cầu (HTTP Requests) tới tập hợp các máy chủ backend thuộc Target Group trải dài trên nhiều **Availability Zones (AZs)**.

---

#### Bảng thông số cấu hình ALB

| Bảng thông số | Giá trị cấu hình | Ý nghĩa / Mục đích |
| :--- | :--- | :--- |
| **Load balancer name** | `fca-web-alb` | Tên nhận diện Load Balancer |
| **Scheme** | `Internet-facing` | Cho phép tiếp nhận kết quả truy cập từ Internet |
| **IP address type** | `IPv4` | Định dạng địa chỉ IP |
| **VPC** | `fca-workshop-vpc` | VPC triển khai hạ tầng |
| **Mappings (AZs)** | `ap-southeast-1a` & `ap-southeast-1b` | Định tuyến Multi-AZ (`fca-public-subnet-a` & `b`) |
| **Security groups** | `workshop-alb-sg` | Bảo mật cấp ALB (cho phép HTTP port 80 từ Internet) |
| **Listeners** | `HTTP : 80` | Lắng nghe kết nối HTTP trên cổng 80 |
| **Default Action** | `Forward to fca-web-target-group` | Chuyển tiếp lưu lượng tới Target Group Flask (port 5000) |

---

#### Các bước thực hiện trên AWS Console

##### Bước 1: Khởi tạo Load Balancer
1. Vào **AWS Management Console** → chọn dịch vụ **EC2**.
2. Ở menu bên trái, cuộn xuống mục **Load Balancing** → chọn **Load Balancers**.
3. Nhấp nút màu cam **Create load balancer**.
4. Chọn loại **Application Load Balancer (ALB)** → nhấp nút **Create**.

##### Bước 2: Cấu hình cơ bản (Basic configuration)
1. **Load balancer name:** Nhập `fca-web-alb`.
2. **Scheme:** Chọn **Internet-facing**.
3. **IP address type:** Chọn **IPv4**.

##### Bước 3: Cấu hình mạng Multi-AZ (Network mapping)
1. **VPC:** Chọn VPC riêng `fca-workshop-vpc`.
2. **Mappings:** Tích chọn 2 Availability Zones khác nhau:
   * Zone **`ap-southeast-1a`** → Chọn Subnet: `fca-public-subnet-a`
   * Zone **`ap-southeast-1b`** → Chọn Subnet: `fca-public-subnet-b`

##### Bước 4: Gán Security Group
1. Tại phần **Security groups**, gỡ chọn Security Group mặc định (`default`).
2. Tích chọn Security Group riêng của ALB: **`workshop-alb-sg`**.  
   *(Lưu ý: Security Group này phải mở Inbound Rule: HTTP Port 80 từ `0.0.0.0/0`).*

##### Bước 5: Cấu hình Listener & Routing Rule
1. Tại phần **Listeners and routing**:
   * **Protocol:** `HTTP`
   * **Port:** `80`
2. Tại phần **Default action**, mở danh sách thả xuống chọn **Forward to** → chọn **`fca-web-target-group`**.

##### Bước 6: Kiểm tra và Khởi tạo
1. Kiểm tra lại toàn bộ thông số trong bảng tóm tắt **Summary**.
2. Nhấp chọn **Create load balancer**.

<p align="center">
  <img src="/images/5-Workshop/5.7-ALB/alb-created.png" alt="Application Load Balancer Created" width="85%" />
  <br>
  <em>Figure 5.14: Application Load Balancer Created Successfully</em>
</p>

---
### 3. Cấu hình Security Groups (Tường lửa Bảo mật)

Để đảm bảo nguyên tắc bảo mật tối thiểu (**Principle of Least Privilege**) và bảo vệ máy chủ ứng dụng, chúng ta cần cấu hình chuỗi Security Groups dạng phân lớp (Layered Security Groups). 

Kiến trúc này đảm bảo máy chủ EC2 **chỉ chấp nhận kết nối HTTP cổng 5000 khi đi qua Application Load Balancer (ALB)**, đồng thời chặn hoàn toàn các truy cập trực tiếp từ Internet vào cổng 5000 của EC2.

---

#### Bảng cấu hình Inbound Rules của Security Groups

##### 1. Security Group dành cho ALB (`workshop-alb-sg`)
| Type | Port Range | Protocol | Source | Mô tả / Mục đích |
| :--- | :--- | :--- | :--- | :--- |
| **HTTP** | `80` | TCP | `0.0.0.0/0` (Anywhere-IPv4) | Cho phép người dùng từ Internet truy cập giao diện Web qua cổng 80 |

##### 2. Security Group dành cho EC2 Web Server (`fca-web-sg`)
| Type | Port Range | Protocol | Source | Mô tả / Mục đích |
| :--- | :--- | :--- | :--- | :--- |
| **SSH** | `22` | TCP | `My IP` | Cho phép Admin SSH quản trị EC2 an toàn từ IP cá nhân |
| **Custom TCP** | `5000` | TCP | `workshop-alb-sg` | Chỉ cho phép lưu lượng truy cập từ ALB đi vào cổng 5000 của Flask |

---

#### Các bước thực hiện trên AWS Console

1. Truy cập **AWS Management Console** → **EC2** → **Security Groups**.
2. Tìm và nhấp chọn Security Group của EC2: **`fca-web-sg`**.
3. Chọn tab **Inbound rules** → Bấm **Edit inbound rules**.
4. Cập nhật quy tắc cho cổng `5000`:
   * Xóa quy tắc IPv4 CIDR cũ (nếu có).
   * Bấm **Add rule**:
     * **Type:** `Custom TCP`
     * **Port range:** `5000`
     * **Source:** Chọn **Custom** → Nhập/chọn mã Security Group của ALB (**`workshop-alb-sg`**).
5. Nhấp nút màu cam **Save rules** để lưu cấu hình.

<p align="center">
  <img src="/images/5-Workshop/5.7-ALB/alb-ec2-sg-rules.png" alt="Configure Security Groups" width="85%" />
  <br>
  <em>Figure 5.15: EC2 Security Group Inbound Rules updated to reference ALB Security Group</em>
</p>

---

### 4. Đăng ký EC2 Instance vào Target Group

Sau khi đã khởi tạo Target Group và thiết lập chuỗi Security Groups bảo mật, bước tiếp theo là đăng ký (register) máy chủ backend EC2 **`fca-web-server-01`** vào **`fca-web-target-group`**. 

Thao tác này giúp Application Load Balancer xác định được danh sách các máy chủ đích sẽ tiếp nhận các yêu cầu HTTP (Port 5000) được chuyển tiếp từ cổng 80 của ALB.

---

#### Bảng thông số Đăng ký Target

| Thông số | Giá trị | Giải thích |
| :--- | :--- | :--- |
| **Target Group** | `fca-web-target-group` | Nhóm Target nhận lưu lượng |
| **Target Instance** | `fca-web-server-01` | Máy chủ EC2 đang chạy ứng dụng Flask |
| **Target Port** | `5000` | Cổng dịch vụ ứng dụng Flask trên EC2 |

---

#### Các bước thực hiện trên AWS Console

1. Truy cập **AWS Management Console** → **EC2** → **Target Groups**.
2. Nhấp chọn **`fca-web-target-group`**.
3. Chọn tab **Targets** → nhấp nút **Register targets**.
4. Tại danh sách **Available instances**, tích chọn **`fca-web-server-01`**.
5. Đảm bảo cổng tiếp nhận là **`5000`**, sau đó bấm **Include as pending below**.
6. Cuộn xuống kiểm tra danh sách trong bảng *Review pending targets* và nhấp chọn **Register pending targets**.

<p align="center">
  <img src="/images/5-Workshop/5.7-ALB/target-registered.png" alt="EC2 Instance Registered with Target Group" width="85%" />
  <em>Figure 5.16: EC2 Instance Successfully Registered with Target Group</em>
</p>

---

### 5. Kiểm tra trạng thái Health của Target

Sau khi đăng ký máy chủ EC2 vào Target Group, bước tiếp theo là kiểm tra trạng thái hoạt động của Target.

Application Load Balancer sử dụng cơ chế **Health Check** đã được cấu hình để định kỳ gửi các yêu cầu HTTP đến máy chủ EC2 đã đăng ký. Target được xác định là hoạt động bình thường khi ứng dụng phản hồi với mã HTTP được yêu cầu.

---

#### Bảng thông số cấu hình Health Check

| Thông số | Cấu hình |
| :--- | :--- |
| **Protocol** | `HTTP` |
| **Path** | `/` |
| **Port** | `Traffic port` (`5000`) |
| **Healthy threshold** | `5` lần thành công liên tiếp |
| **Unhealthy threshold** | `2` lần thất bại liên tiếp |
| **Timeout** | `5` giây |
| **Interval** | `30` giây |
| **Success codes** | `200` |

---

#### Các bước thực hiện trên AWS Console

##### Bước 1: Mở Target Group
1. Truy cập **AWS Management Console** → **EC2**.
2. Tại menu bên trái, chọn **Target Groups**.
3. Chọn **`fca-web-target-group`**.
4. Mở tab **Targets**.

##### Bước 2: Kiểm tra trạng thái Target
Tìm máy chủ EC2 **`fca-web-server-01`**. Trạng thái của Target được hiển thị tại cột **Health status**.

Khi ứng dụng Flask đang hoạt động bình thường và cấu hình mạng cho phép ALB kết nối đến port 5000, trạng thái của Target sẽ chuyển thành **`Healthy`**.

| Thông số | Giá trị |
| :--- | :--- |
| **Target** | `fca-web-server-01` |
| **Port** | `5000` |
| **Health status** | `Healthy` |

> **Lưu ý:** Trạng thái ban đầu có thể hiển thị là `Initial` hoặc `Unhealthy`. Hãy chờ một vài chu kỳ Health Check và tải lại trang để cập nhật trạng thái mới nhất.

<p align="center">
  <img src="/images/5-Workshop/5.7-ALB/target-healthy.png" alt="Healthy Target in Target Group" width="85%" />
  <br>
  <em>Figure 5.17: Trạng thái Health của EC2 Instance là Healthy</em>
</p>

##### Bước 3: Kiểm tra thông tin chi tiết Health Check
Nhấp chọn Target EC2 để xem thông tin chi tiết về Health Check. Target cần trả về Health Check thành công với mã HTTP **`200`**.

Điều này xác nhận Application Load Balancer có thể kết nối thành công đến ứng dụng Flask đang chạy trên EC2 thông qua port 5000.

<p align="center">
  <img src="/images/5-Workshop/5.7-ALB/target-health-details.png" alt="Target Health Check Details" width="85%" />
  <br>
  <em>Figure 5.18: Chi tiết Health Check của Target</em>
</p>