---
title: "Application Load Balancer (ALB)"
date : 2024-01-01
weight : 7
chapter : false
pre : " <b> 5.7. </b> "
---

## 1. Create a Target Group

Before configuring the **Application Load Balancer (ALB)** to route incoming traffic, we must first establish a **Target Group**. The Target Group acts as a logical grouping of backend resources (such as EC2 instances) and routinely monitors their operational status via **Health Checks**.

---

### Configuration Parameters

| Parameter | Configuration Value | Description |
| :--- | :--- | :--- |
| **Target type** | `Instances` | Route traffic directly to EC2 instances |
| **Target group name** | `fca-web-target-group` | Unique identifier for the Target Group |
| **Protocol** | `HTTP` | Protocol for web requests |
| **Port** | `5000` | Port listening on the backend Flask app |
| **IP address type** | `IPv4` | IP address standard |
| **VPC** | `fca-workshop-vpc` | VPC hosting the infrastructure |
| **Health check path** | `/` | Endpoint URL used for health probes |

---

### AWS Hands-On Implementation

#### Step 1: Access the Target Groups Dashboard
1. Open the **AWS Management Console** and navigate to **EC2**.
2. On the left navigation pane, under **Load Balancing**, select **Target Groups**.
3. Click **Create target group**.

#### Step 2: Select Target Type and Basic Settings
1. Under **Choose a target type**, select **Instances**.
2. Enter the configuration settings:
   * **Target group name:** `fca-web-target-group`
   * **Protocol:** `HTTP`
   * **Port:** `5000`
   * **VPC:** Select `fca-workshop-vpc`

#### Step 3: Configure Health Checks
1. Under **Health checks**:
   * **Health check protocol:** `HTTP`
   * **Health check path:** `/`
2. Leave all advanced health check settings as default.
3. Click **Next**.

#### Step 4: Finalize Target Group Creation
1. On the **Register targets** screen, skip registering EC2 instances for now (registration will be performed in Step 5.7.4).
2. Scroll to the bottom and click **Create target group**.


### 2. Configure the Application Load Balancer (ALB)

The **Application Load Balancer (ALB)** functions as the single public-facing entry point for user traffic. It automatically distributes incoming HTTP requests across backend instances managed within a Target Group across multiple **Availability Zones (AZs)**.

---

#### ALB Configuration Parameters

| Parameter | Configuration Value | Description |
| :--- | :--- | :--- |
| **Load balancer name** | `fca-web-alb` | Unique ALB identifier |
| **Scheme** | `Internet-facing` | Routes public internet requests |
| **IP address type** | `IPv4` | Standard IPv4 protocol |
| **VPC** | `fca-workshop-vpc` | Target VPC network |
| **Mappings (AZs)** | `ap-southeast-1a` & `ap-southeast-1b` | Multi-AZ mapping (`fca-public-subnet-a` & `b`) |
| **Security groups** | `fca-alb-sg` | Controls incoming traffic (Allows HTTP port 80) |
| **Listeners** | `HTTP : 80` | Listens for client connections on Port 80 |
| **Default Action** | `Forward to fca-web-target-group` | Forwards traffic to Flask Target Group (Port 5000) |

---

### AWS Hands-On Implementation

#### Step 1: Initialize Load Balancer Creation
1. Access the **AWS Management Console** → Navigate to **EC2**.
2. In the left navigation pane under **Load Balancing**, click **Load Balancers**.
3. Click **Create load balancer**.
4. Under **Application Load Balancer**, click **Create**.

#### Step 2: Basic Configuration
1. **Load balancer name:** Enter `fca-web-alb`.
2. **Scheme:** Select **Internet-facing**.
3. **IP address type:** Select **IPv4**.

#### Step 3: Multi-AZ Network Mapping
1. **VPC:** Select `fca-workshop-vpc`.
2. **Mappings:** Select two distinct Availability Zones:
   * **`ap-southeast-1a`** → Select Subnet: `fca-public-subnet-a`
   * **`ap-southeast-1b`** → Select Subnet: `fca-public-subnet-b`

#### Step 4: Assign Security Group
1. Under **Security groups**, remove the `default` security group.
2. Select **`fca-alb-sg`**.

#### Step 5: Configure Listener and Routing
1. Under **Listeners and routing**:
   * **Protocol:** `HTTP`
   * **Port:** `80`
2. Under **Default action**, set **Forward to** → `fca-web-target-group`.

#### Step 6: Review and Create
1. Review all parameters in the **Summary** pane.
2. Click **Create load balancer**.

<p align="center">
  <img src="/images/5-Workshop/5.7-ALB/alb-created.png" alt="Application Load Balancer Created" width="85%" />
  <br>
  <em>Figure 5.14: Application Load Balancer Created Successfully</em>
</p>


### 3. Configure Security Groups

To enforce the principle of least privilege and establish a robust security boundary, we configure layered **Security Groups**. 

This multi-tier security design guarantees that the EC2 backend instance **only accepts HTTP traffic on Port 5000 routed through the Application Load Balancer (ALB)**, while blocking all direct public access to Port 5000.

---

### Security Flow Architecture

```text
[ Public Internet Users ]
        │
        │ HTTP (Port 80)
        ▼
[ Application Load Balancer ] ── (Security Group: workshop-alb-sg)
        │
        │ Custom TCP (Port 5000) ── [Restricted to workshop-alb-sg]
        ▼
[ EC2 Web Server Instance ]  ── (Security Group: fca-web-sg)
```
<p align="center">
  <img src="/images/5-Workshop/5.7-ALB/alb-ec2-sg-rules.png" alt="Configure Security Groups" width="85%" />
  <br>
  <em>Figure 5.15: Configure Security Groups</em>
</p>

## 4. Register EC2 Instance with the Target Group

After establishing the Target Group and layered Security Groups, the next step is to register the backend EC2 server **`fca-web-server-01`** into **`fca-web-target-group`**. 

This registration enables the Application Load Balancer to recognize active backend targets for receiving forwarded HTTP requests on Port 5000.

---

### Target Registration Parameters

| Parameter | Value | Description |
| :--- | :--- | :--- |
| **Target Group** | `fca-web-target-group` | Destination Target Group |
| **Target Instance** | `fca-web-server-01` | EC2 instance hosting the Flask app |
| **Target Port** | `5000` | Application port listening on EC2 |

---

### AWS Hands-On Implementation Steps

1. Navigate to **AWS Management Console** → **EC2** → **Target Groups**.
2. Select **`fca-web-target-group`**.
3. Navigate to the **Targets** tab and click **Register targets**.
4. In the **Available instances** list, check **`fca-web-server-01`**.
5. Confirm the target port is set to **`5000`**, then click **Include as pending below**.
6. Review the target list under *Review pending targets* and click **Register pending targets**.

<p align="center">
  <img src="/images/5-Workshop/5.7-ALB/target-registered.png" alt="EC2 Instance Registered with Target Group" width="85%" />
  <br>
  <em>Figure 5.16: EC2 Instance Successfully Registered with Target Group</em>
</p>

### 5. Verify Target Health

After registering the EC2 instance with the Target Group, the next step is to verify whether the target is healthy.

The Application Load Balancer uses the configured **Health Check** to periodically send HTTP requests to the registered EC2 instance. The target is considered healthy when the application responds with the expected HTTP status code.

For this workshop, the Health Check is configured as follows:

| Parameter | Configuration |
| :--- | :--- |
| **Protocol** | `HTTP` |
| **Path** | `/` |
| **Port** | `Traffic port` (`5000`) |
| **Healthy threshold** | `5` consecutive successes |
| **Unhealthy threshold** | `2` consecutive failures |
| **Timeout** | `5` seconds |
| **Interval** | `30` seconds |
| **Success codes** | `200` |

### Step 1: Open the Target Group

1. Access **AWS Management Console** → **EC2**.
2. In the left navigation pane, select **Target Groups**.
3. Select **`fca-web-target-group`**.
4. Open the **Targets** tab.

### Step 2: Check the Target Status

Locate the registered instance:

```text
fca-web-server-01
```
The target status is displayed in the Health status column.

When the Flask application is running correctly and the network configuration allows the ALB to reach port 5000, the target status should become:

Healthy

The target should have the following configuration:

Parameter	Value
Target	fca-web-server-01
Port	5000
Health status	Healthy
<p align="center"> <img src="/images/5-Workshop/5.7-ALB/target-healthy.png" alt="Healthy Target in Target Group" width="85%" /> <br> <em>Figure 5.17: EC2 Instance Health Status is Healthy</em> </p>

Note: The health status may initially appear as Initial or Unhealthy. Wait for several health check cycles and refresh the page to obtain the latest status.

Step 3: Verify the Health Check Details

Click the target instance to view the health check details.

The target should report a successful health check with HTTP status code:

200

This confirms that the ALB can successfully communicate with the Flask application running on the EC2 instance through port 5000.

<p align="center"> <img src="/images/5-Workshop/5.7-ALB/target-health-details.png" alt="Target Health Check Details" width="85%" /> <br> <em>Figure 5.18: Target Health Check Details</em> </p> ```