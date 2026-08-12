---
title : "Deploy the Python Web Application"
date : 2024-01-01
weight : 4
chapter : false
pre : " <b> 5.4. </b> "
---

#### 1. Prepare the Python Web Application

Before deploying the application to Amazon EC2, a simple Python web application is prepared and tested locally.

The application is developed using the **Flask** framework. It provides a simple web interface and displays information identifying the server that handles the request.

The application displays the following information:

* Application name
* Hostname
* EC2 Instance ID

This information will later be used to verify traffic distribution between multiple EC2 instances through the **Application Load Balancer**.

The project contains the following files:

```text
fca-aws-workshop/
├── app.py
└── requirements.txt
```

The Flask application is configured to listen on `0.0.0.0` and port `5000` so that it can receive network connections after being deployed to an EC2 instance.

The application is first tested locally to verify that it runs successfully before deployment to AWS.

**Figure 5.5. Python Web Application Source Code**

![Python Web Application Source Code](/images/5-Workshop/5.2-Prerequisite/python-project.png)

After starting the Flask application, the web interface is accessed through the local address `http://127.0.0.1:5000`.

**Figure 5.6. Local Test of the Python Web Application**

![Local Test of the Python Web Application](/images/5-Workshop/5.4-Deloy-python/python-local-test.png)

#### 2. Launch an EC2 Instance

After preparing and testing the Python web application locally, an Amazon EC2 instance is launched to host the application.

Navigate to:

**AWS Management Console → EC2 → Instances → Launch instances**

The EC2 instance is configured with the following parameters:

| Configuration | Value |
|---|---|
| **Instance name** | `fca-web-server-01` |
| **Operating System** | Ubuntu |
| **Instance type** | `t3.micro` |
| **VPC** | `fca-workshop-vpc` |
| **Subnet** | `fca-public-subnet-a` |
| **Availability Zone** | `ap-southeast-1a` |
| **Public IP** | Enabled |
| **Key Pair** | `fca-workshop-key` |
| **Security Group** | `fca-web-sg` |

The EC2 instance is deployed in `ap-southeast-1a` and is assigned a public IP address for initial administration and application testing.

The security group allows SSH access from the administrator's IP address. TCP port 5000 is also temporarily allowed from the administrator's IP address for testing the Flask application during the deployment phase.

After reviewing the configuration, the instance is launched.

**Figure 5.7. EC2 Instance Configuration**
![EC2 Instance Configuration](/images/5-Workshop/5.4-Deloy-python/ec2-instance-created.png)

The network configuration of the instance is then verified to ensure that it is connected to the correct VPC and subnet.

**Figure 5.8. EC2 Network Configuration**
![EC2 Network Configuration](/images/5-Workshop/5.4-Deloy-python/ec2-network-configuration.png)

#### 3. Connect to the EC2 Instance and Install the Python Environment

After launching the EC2 instance, an SSH connection is established to access the Ubuntu server and prepare the Python environment.

The EC2 instance is accessed using the **EC2 Key Pair** created during the prerequisite stage.

The SSH connection uses the Ubuntu default user:

```text
ubuntu
```

After successfully connecting to the instance, the operating system and Python environment are verified.

The required Python packages are installed using the following command:

```bash
sudo apt update
sudo apt upgrade -y
sudo apt install -y python3 python3-pip python3-venv
```

A dedicated directory is then created for the application:

```bash
mkdir -p ~/fca-aws-workshop
cd ~/fca-aws-workshop
```

A Python virtual environment is created to isolate the application's dependencies:

```bash
python3 -m venv venv
source venv/bin/activate
```

The Python environment is then ready for deploying the Flask application.

**Figure 5.9. SSH Connection to the EC2 Instance**
![SSH Connection to the EC2 Instance](/images/5-Workshop/5.4-Deloy-python/ec2-ssh-connection.png)

**Figure 5.10. Python Environment on EC2**
![Python Environment on EC2](/images/5-Workshop/5.4-Deloy-python/python-environment-ec2.png)


#### 4. Deploy and Run the Python Web Application

After preparing the Python environment on the EC2 instance, the **Python Web Application** is deployed to the server.

The application source code is transferred from the local development environment to the EC2 instance.

The application consists of the following files:

```text
fca-aws-workshop/
├── app.py
└── requirements.txt

The files are uploaded to the application directory:

/home/ubuntu/fca-aws-workshop/

After uploading the source code, activate the Python virtual environment:

source venv/bin/activate

Install the required Python dependencies using the requirements.txt file:

pip install -r requirements.txt

After the installation is completed, start the Flask application:

python app.py

The application is configured to listen on 0.0.0.0 and port 5000. This allows the web application to receive network connections from outside the EC2 instance.

When the application starts successfully, the terminal displays a message similar to:

Running on all addresses (0.0.0.0)
Running on http://127.0.0.1:5000

This confirms that the Flask Web Application is running successfully on the EC2 instance.

Figure 5.11. Python Web Application Running on EC2

5.4.4.1. Test the Python Web Application

After starting the Flask application, the web application is tested through the Public IPv4 address of the EC2 instance.

Access the application using the following address:

http://<EC2-Public-IP>:5000

The web page displays the application interface together with the Hostname and Instance ID information.

The successful display of the web page confirms that the Python Web Application has been successfully deployed and is accessible from outside the EC2 instance.

The server identification information will be used in the following stages to verify traffic distribution between multiple EC2 instances through the Application Load Balancer.

Figure 5.12. Python Web Application Accessed from EC2