📘 High Availability Application Using Infrastructure as Code (CloudFormation)

This project demonstrates how to design, automate, and deploy a highly available web application on AWS using Infrastructure as Code (IaC) with AWS CloudFormation.
It includes reusable, modular templates for the network layer and application layer, along with deployment and teardown scripts for full automation.

The application follows best practices for scalability, high availability, and security, using services such as:

Amazon VPC

Public & Private Subnets

Application Load Balancer (ALB)

Auto Scaling Group (ASG)

Launch Templates

EC2 Instances

S3 Bucket for static content

Security Groups

CloudFormation Nested / Imported Outputs

🔧 Project Architecture

The infrastructure is divided into two CloudFormation stacks:

1. Network Stack

Creates the foundational network resources:

VPC

Internet Gateway & Route Tables

Public Subnets

Private Subnets

Required networking outputs (exported for use by the application stack)

2. Application (Udagram) Stack

Deploys the application layer:

Launch Template (EC2 + User Data)

Auto Scaling Group in private subnets

Application Load Balancer in public subnets

Target Group and Listener (port 80)

Security Groups following least-privilege

S3 bucket hosting static files pulled by EC2 instances

🚀 Deployment Instructions
1. Deploy Network Stack
./create.sh udagram-network-stack network.yml network-parameters.json

2. Deploy Application Stack
./create.sh udagram-app-stack udagram.yml udagram-parameters.json

🧹 Delete/Teardown Instructions
1. Delete Application Stack
./delete.sh udagram-app-stack

2. Delete Network Stack
./delete.sh udagram-network-stack

🌐 Working Demo (Live URLs)
Load Balancer URL

http://udagra-webap-c1guah7clfo2-1176945879.us-east-1.elb.amazonaws.com/

S3 Static Web Content

http://udagram-server-infrastructure-static-content.s3-website-us-east-1.amazonaws.com

The Load Balancer serves the static content pulled from the S3 bucket and rendered by EC2 instances.

📸 Evidence of Work (Required for Project)
Option 1 (Used): Live URLs Provided

If required for evaluation, the following screenshots are also included in the repository:

CloudFormation Output (Network + App stack)

Successful access via Load Balancer

S3 bucket content page

🛡 Security Best Practices Implemented

All traffic flows through ALB

EC2 instances are not publicly accessible

Security groups follow least-privilege

Application runs in private subnets

Automated scaling for high availability

📂 Repository Structure
📁 High-Availability-Application-Using-Infrastructure-as-Code-CloudFormation
│── README.md
│── network.yml
│── network-parameters.json
│── udagram.yml
│── udagram-parameters.json
│── create.sh
│── update.sh
│── delete.sh
│── /screenshots
│── /static-content (optional)

📝 Submission Notes

Please pay particular attention to:

Imported values between network and application stack

Auto Scaling Group configuration

Security group least-privilege rules

Load balancer + listener + target group correctness

EC2 user-data pulling content from S3
