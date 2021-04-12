# AWS
## AWS services
- **Compute services**: Amazon EC2, AWS Eleastic Beanstalk, Lambda
- **File Storage Service**: S3 (host  website to Amazon)
- **Content and Network Delivery services**: Amazon VPC and Direct Connect, Route 53, Elastic Load Balancing, CloudFront and API Gateway, Global Accelerator
- **Database Service and Ultilities**: RDS, DynamoDB, Elasticache and Redshift
- **App Intergration Services**: Messaging Services, Step Function
- **Management and Governance Services**: CloudTrail, CloudWatch and AWS Config, Systems Manager, CloudFormation, OpsWorks, Organizations and Control Tower

## EC2
- A Web service that provides resizable compute capacity in the cloud. It is designed to make web-scale computing easier for developers
- Usage:
	- Web application hosting
	- Batch processing 
	- API server
	- Desktop in the cloud
- EC2 concept:
	- Instance Types: 
		- Defines the processor, memory, and storage type. Cannot be change without downtime
		- Category:
			- General purpose
			- Compute, memory, and storage optimized
			- Accelerated computing
	- Root Device Type:
			- Instance Store: Ephemeral storage physically attached to the host he virtual server is running on. Completely shut down: data go away
			- Elastic Block Store (most used): Persistent storage that exists separately from the host the virtual server is running on. Completely shut down: data will be persited. We can take a snapshop and copy it
	- Amazon Machine Image AMI:
		- Templatefor an EC2 instance including config, operating system, and data
		- Custom AMI can be build base on our config
		- Can be sharedd across AWS account

## Host a web server
- Launch an EC2 instance
- Choose Amazon Linux2 AMI, general purpose t2 micro
- Auto-assign public = enable
- Next -> Network interfaces -> Advanced details User data, run a code that'll start the server
```
#!/bin/bash
yum install httpd -y
service httpd start
```
- Next -> sercurity group -> SSH, Source: My IP so only user can access to the dashboard && HTTP Source: Custom so anyone can access to the server
- Create a key pair
- In the instance, go to public DNS -> go to website

## Deploy S3
- Upload file
- Change permission to public access everyone read object
- Go to bucket -> property -> Static website hosting -> use this bucket to host -> save
- Change permission to public access everyone read object
 for index.html

## Deploy SpringBoot to AWS EC2 using S3
- Spring Boot app ```mvn clean install```

- EC2 -> Running Instance -> Launch Instance -> select Instance type -> Launch -> Key pair: AWS_AMI_instance_1 -> Launch -> top: connect -> Standalone SSH client -> connect using PuTTY -> PuTTY Load AWS Instance 1 Hostname: ec2-user@ec2...amazonaws.com -> SSH -> Auth : browse private key -> install java same version as our SpringBoot app

- Create S3 Bucket -> remove block all public access -> tick achknowlede -> create bucket -> create folder-> upload -> our maven exported Snapshot .jar file -> success -> copy object url -> make public

- PuTTY -> in root directory -> wget paste url -> ls to check if jar file there -> java -jar downloaded..SNAPSHOT.jar

- EC2 -> security group -> inbound -> anywhere -> go to instance -> copy Public DNS url -> paste -> page runs

