---
title: "Triển khai ứng dụng Web Python"
date : 2024-01-01
weight : 4
chapter : false
pre : " <b> 5.4. </b> "
---

#### 1. Chuẩn bị ứng dụng Web Python

Trước khi triển khai ứng dụng lên Amazon EC2, một ứng dụng Web đơn giản được xây dựng bằng Python và kiểm tra trên máy local.

Ứng dụng được phát triển bằng framework **Flask**. Ứng dụng cung cấp một giao diện Web đơn giản và hiển thị thông tin xác định máy chủ đang xử lý request.

Ứng dụng hiển thị các thông tin:

* Tên ứng dụng
* Hostname
* EC2 Instance ID

Các thông tin này sẽ được sử dụng để kiểm tra khả năng phân phối lưu lượng giữa nhiều EC2 instance thông qua **Application Load Balancer**.

Project bao gồm các file:

```text
fca-aws-workshop/
├── app.py
└── requirements.txt
```

Ứng dụng Flask được cấu hình lắng nghe trên `0.0.0.0` và port `5000` để có thể nhận kết nối mạng sau khi được triển khai trên EC2.

Trước khi triển khai lên AWS, ứng dụng được chạy thử trên máy local để đảm bảo ứng dụng hoạt động bình thường.

**Hình 5.5. Source Code của ứng dụng Web Python**
![Source Code của ứng dụng Web Python](/images/5-Workshop/5.2-Prerequisite/python-project.png)

Sau khi khởi động ứng dụng Flask, truy cập giao diện Web thông qua địa chỉ local `http://127.0.0.1:8000`.

**Hình 5.6. Kiểm tra ứng dụng Web Python trên máy local**

![Kiểm tra ứng dụng Web Python trên máy local](/images/5-Workshop/5.4-Deloy-python/python-local-test.png)

#### 2. Khởi tạo EC2 Instance

Sau khi chuẩn bị và kiểm tra ứng dụng Web Python trên máy local, một Amazon EC2 instance được khởi tạo để triển khai ứng dụng.

Truy cập:

**AWS Management Console → EC2 → Instances → Launch instances**

EC2 instance được cấu hình với các thông số:

| Cấu hình | Giá trị |
|---|---|
| **Tên instance** | `fca-web-server-01` |
| **Hệ điều hành** | Ubuntu |
| **Instance type** | `t3.micro` |
| **VPC** | `fca-workshop-vpc` |
| **Subnet** | `fca-public-subnet-a` |
| **Availability Zone** | `ap-southeast-1a` |
| **Public IP** | Enabled |
| **Key Pair** | `fca-workshop-key` |
| **Security Group** | `fca-web-sg` |

EC2 instance được triển khai tại `ap-southeast-1a` và được cấp Public IP để phục vụ việc quản trị ban đầu và kiểm tra ứng dụng.

Security Group cho phép SSH từ địa chỉ IP của quản trị viên. Port TCP 5000 cũng được tạm thời cho phép từ địa chỉ IP của quản trị viên để kiểm tra ứng dụng Flask trong quá trình triển khai.

Sau khi kiểm tra các thông số, tiến hành khởi tạo EC2 instance.

**Hình 5.7. Cấu hình EC2 Instance**

![Cấu hình EC2 Instance](/images/5-Workshop/5.4-Deloy-python/ec2-instance-created.png)
Sau đó kiểm tra cấu hình mạng của instance để đảm bảo EC2 được kết nối đúng VPC và subnet.

**Hình 5.8. Cấu hình mạng của EC2**
![Cấu hình mạng của EC2](/images/5-Workshop/5.4-Deloy-python/ec2-network-configuration.png)

#### 3. Kết nối EC2 và cài đặt môi trường Python

Sau khi khởi tạo EC2 instance, tiến hành kết nối SSH để truy cập máy chủ Ubuntu và chuẩn bị môi trường Python.

EC2 instance được truy cập bằng **EC2 Key Pair** đã được tạo trong phần điều kiện tiên quyết.

Kết nối SSH sử dụng user mặc định của Ubuntu:

```text
ubuntu
```

Sau khi kết nối thành công, tiến hành kiểm tra hệ điều hành và môi trường Python.

Các package Python cần thiết được cài đặt bằng các lệnh:

```bash
sudo apt update
sudo apt upgrade -y
sudo apt install -y python3 python3-pip python3-venv
```

Tiếp theo, tạo thư mục riêng cho ứng dụng:

```bash
mkdir -p ~/fca-aws-workshop
cd ~/fca-aws-workshop
```

Tạo Python virtual environment để cô lập các thư viện của ứng dụng:

```bash
python3 -m venv venv
source venv/bin/activate
```

Sau khi hoàn thành, môi trường Python đã sẵn sàng để triển khai ứng dụng Flask.

**Hình 5.9. Kết nối SSH đến EC2 Instance**

![Kết nối SSH đến EC2 Instance](/images/5-Workshop/5.4-Deloy-python/ec2-ssh-connection.png)

**Hình 5.10. Môi trường Python trên EC2**

![Môi trường Python trên EC2](/images/5-Workshop/5.4-Deloy-python/python-environment-ec2.png)


#### 4. Triển khai và chạy ứng dụng Web Python

Sau khi hoàn thành việc chuẩn bị môi trường Python trên EC2 instance, **ứng dụng Web Python** được triển khai lên máy chủ.

Source code của ứng dụng được tải từ môi trường phát triển local lên EC2 instance.

Ứng dụng bao gồm các file:

```
fca-aws-workshop/
├── app.py
└── requirements.txt
```

Các file được tải lên thư mục ứng dụng:

```
/home/ubuntu/fca-aws-workshop/
```

Sau khi tải source code lên EC2, kích hoạt Python virtual environment:

```
source venv/bin/activate
```

Tiếp theo, cài đặt các thư viện cần thiết từ file requirements.txt:

```
pip install -r requirements.txt
```

Sau khi quá trình cài đặt hoàn tất, khởi chạy ứng dụng Flask:

```
python app.py
```

Ứng dụng được cấu hình lắng nghe trên 0.0.0.0 và port 5000. Cấu hình này cho phép ứng dụng Web nhận các kết nối mạng từ bên ngoài EC2 instance.

Khi ứng dụng khởi động thành công, Terminal hiển thị thông báo tương tự:

``` 
Running on all addresses (0.0.0.0)
Running on http://127.0.0.1:5000
```

Điều này xác nhận ứng dụng Web Flask đã được khởi chạy thành công trên EC2 instance.

**Hình 5.11. Ứng dụng Web Python đang chạy trên EC2**
![Ứng dụng Web Python đang chạy trên EC2](/images/5-Workshop/5.4-Deloy-python/python-app-running.png)


#### 5. Kiểm tra ứng dụng Web Python

Sau khi khởi chạy ứng dụng Flask, tiến hành kiểm tra ứng dụng thông qua Public IPv4 của EC2 instance.

Truy cập ứng dụng bằng địa chỉ:

```
http://<EC2-Public-IP>:5000
```

Trang Web hiển thị giao diện của ứng dụng cùng với thông tin Hostname và Instance ID.

Việc trang Web được hiển thị thành công xác nhận ứng dụng Web Python đã được triển khai thành công và có thể truy cập từ bên ngoài EC2 instance.

Thông tin xác định máy chủ sẽ được sử dụng ở các bước tiếp theo để kiểm tra khả năng phân phối lưu lượng giữa nhiều EC2 instance thông qua Application Load Balancer.

**Hình 5.12. Truy cập ứng dụng Web Python trên EC2**
![Truy cập ứng dụng Web Python trên EC2](/images/5-Workshop/5.4-Deloy-python/python-app-ec2-browser.png)