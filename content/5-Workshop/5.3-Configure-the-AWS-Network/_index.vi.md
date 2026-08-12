---
title: "Cấu hình Mạng AWS"
date : 2024-01-01
weight : 3
chapter : false
pre : " <b> 5.3. </b> "
---


### Bước 1 Tạo VPC

Bước đầu tiên trong quá trình xây dựng hạ tầng mạng AWS là tạo một **Amazon Virtual Private Cloud (VPC)**.

VPC cung cấp một mạng ảo riêng biệt cho các tài nguyên AWS được sử dụng trong workshop. Các tài nguyên của ứng dụng sẽ được triển khai bên trong VPC này ở các bước tiếp theo.

Truy cập:

**AWS Management Console → VPC → Your VPCs → Create VPC**

Tại mục **Resources to create**, chọn:

**VPC only**

Cấu hình VPC như sau:

| Cấu hình | Giá trị |
|---|---|
| **Name tag** | `fca-workshop-vpc` |
| **IPv4 CIDR block** | `10.0.0.0/16` |
| **IPv6 CIDR block** | No IPv6 CIDR block |
| **Tenancy** | Default |

Sau khi hoàn tất cấu hình, chọn **Create VPC**.

Kiểm tra VPC vừa tạo tại **Your VPCs**. VPC phải có trạng thái **Available** và hiển thị đúng IPv4 CIDR đã cấu hình.

**Hình 5.3. Cấu hình VPC**
![VPC Configuration](/images/5-workshop/5.3/vpc-created.png)

### Bước 2 Tạo Subnet
Sau khi tạo VPC, hai subnet được tạo tại các **Availability Zone** khác nhau.

Việc phân bố subnet trên nhiều Availability Zone tạo nền tảng mạng cho việc triển khai các tài nguyên ứng dụng với khả năng sẵn sàng và khả năng chịu lỗi tốt hơn.

Các subnet được tạo bên trong `fca-workshop-vpc`:

| Subnet | Availability Zone | IPv4 CIDR |
|---|---|---|
| `fca-public-subnet-a` | `ap-southeast-1a` | `10.0.1.0/24` |
| `fca-public-subnet-b` | `ap-southeast-1b` | `10.0.2.0/24` |

Subnet thứ nhất được tạo tại `ap-southeast-1a` với CIDR `10.0.1.0/24`.

Subnet thứ hai được tạo tại `ap-southeast-1b` với CIDR `10.0.2.0/24`.

Sau khi tạo xong hai subnet, kiểm tra lại cấu hình tại **VPC → Subnets**.

**Hình 5.4. Các Subnet được phân bố trên hai Availability Zone**
![Các Subnet được phân bố trên hai Availability Zone](/images/5-Workshop/5.3/subnets-created.png)

### Bước 3 Tạo Internet Gateway và Route Table 
Sau khi tạo VPC và các Subnet, bước tiếp theo là cấu hình Internet Gateway (IGW) và Route Table để cho phép các tài nguyên trong Public Subnet kết nối với Internet. Đây là bước cần thiết để EC2 có thể truy cập Internet và người dùng có thể truy cập ứng dụng Web.

#### Tạo Internet Gateway 
1. Truy cập AWS Console → VPC.
2. Chọn Internet gateways ở menu bên trái.
3. Chọn Create internet gateway.
4. Nhập tên:
```workshop-igw```
5. Chọn Create internet gateway.
![InternetGateway](/images/5-Workshop/5.3/internetgateway.png)
**Hình 5.5 Internet Gatewway đã được tạo**
####  Gắn Internet Gateway vào VPC
1. Chọn Internet Gateway vừa tạo.
2. Chọn Actions → Attach to a VPC.
3. Tại Available VPCs, chọn VPC đã tạo ở bước trước.
4. Chọn Attach internet gateway.
![Gắn internet gateway vào vpc](/images/5-Workshop/5.3/igwtovpc.png)
**Hình 5.6 Internet Gateway đã được gắn vào VPC**

#### Tạo Route Table 
1. Trong VPC Console, chọn Route tables.
2. Chọn Create route table.
3. Nhập:
- Name: ```workshop-public-rt```
- VPC: chọn VPC của Workshop.
4. Chọn Create route table.
![route-table](/images/5-Workshop/5.3/route-table.png)
**Hình 5.7 Route Table đã được tạo**

#### Thêm Internet Route 
Chọn ```workshop-public-rt``` → tab Routes → Edit routes → Add route.

Cấu hình:
``` 
Destination: 0.0.0.0/0
Target: Internet Gateway
        workshop-igw 
```
Sau đó chọn Save changes.

Route **0.0.0.0/0** cho phép lưu lượng từ Public Subnet được định tuyến ra Internet thông qua Internet Gateway.
![add-internet-route](/images/5-Workshop/5.3/add-internet-route.png)
**Hình 5.8 Đã thêm Internet Route** 

#### Gắn Route Table với Public Subnet
1. Chọn tab Subnet associations.
2. Chọn Edit subnet associations.
3. Chọn các Public Subnet đã tạo.
4. Chọn Save associations.

![Gắn rt với public subnet](/images/5-Workshop/5.3/rt-to-subnet.png)

**Hình 5.9 Đã gắn Route Table với Public Subnet**

### Kiểm tra 
Sau khi hoàn thành, kiểm tra lại:

- Internet Gateway ở trạng thái Attached.
- Route Table đã có route 0.0.0.0/0.
- Route Table được liên kết với các Public Subnet.
- Public Subnet sử dụng đúng Route Table.

*Kết quả:* Public Subnet đã có đường kết nối Internet thông qua Internet Gateway, tạo cơ sở để triển khai EC2 và Application Load Balancer trong các bước tiếp theo.