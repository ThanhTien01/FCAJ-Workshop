---
title: "Configure Amazon RDS and Amazon S3"
date: 2024-01-01
weight: 5
chapter: false
pre: " <b> 5.5. </b> "
---

In this step, **Amazon RDS** is used to store application data, while **Amazon S3** is used to store files and assets. Separating data from EC2 instances makes the application easier to scale and manage when deploying multiple EC2 instances.

### 1. Configure Amazon RDS
#### Step 1: Create the Database
1. Open the AWS Console → RDS.
2. Select Databases → Create database.
3. Choose:
- Creation method: Standard create.
- Engine: MySQL.
- Template: Free tier.
4. In Settings, enter:
```
DB instance identifier: workshop-db
Master username: admin
Master password: ********
```
5. Under Connectivity:
- Select the VPC you created.
- Choose an appropriate DB Subnet Group.
- Do not enable Public access if the database is only used by EC2 instances.
6. In VPC Security Group, choose the Database Security Group or create a new one.
7. Click Create database.

#### Step 2: Configure Security Group for RDS
To secure the database, allow MySQL connections only from the EC2 Security Group.

Inbound Rule example:
```
Type: MySQL/Aurora
Protocol: TCP
Port: 3306
Source: EC2 Security Group
```
Do not open port 3306 to the public Internet.

#### Step 3: Verify RDS
After the database becomes Available, select the Database and note the:
```
Endpoint
Port
```
Example:
```
Endpoint: workshop-db.xxxxx.ap-southeast-1.rds.amazonaws.com
Port: 3306
```
Use this Endpoint to configure the database connection in your Python application.

![RDS](/images/5-Workshop/5.5/rds.png)
**Figure: RDS instance created**

### 2. Configure Amazon S3
Amazon S3 is used to store application files or assets such as images, uploaded files, or static data.

#### Step 1: Create an S3 Bucket
1. Open the AWS Console → S3.
2. Click Create bucket.
3. Provide a unique bucket name:
```
workshop-high-availability-<unique-id>
```
4. Select the AWS Region that matches your workshop Region.
5. Keep Block all public access enabled.
6. Click Create bucket.

#### Step 2: Upload objects
1. Open the newly created bucket.
2. Click Upload.
3. Select the files or folders to store.
4. Click Upload.

After uploading, files will be stored in Amazon S3 instead of directly on EC2.

#### Step 3: Verify the Bucket
Check that:

- The bucket was created successfully.
- Files were uploaded.
- The bucket is in the correct Region.
- Access permissions are configured appropriately.

![S3](/images/5-Workshop/5.5/s3.png)
**Figure: Amazon S3 bucket**

### Result

After completing these steps, the system can be organized as follows:

```

                  Python Web Application
                           │
                 ┌─────────┴─────────┐
                 ▼                   ▼
            Amazon RDS           Amazon S3
            Database             File Storage
```

Using RDS for the database and S3 for file storage separates data from EC2 instances. When Auto Scaling launches new EC2 instances, they can share the same centralized database and the centrally stored files, which supports the goal of building a High Availability system.
