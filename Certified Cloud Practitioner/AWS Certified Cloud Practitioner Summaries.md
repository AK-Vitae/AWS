# AWS Certified Cloud Practitioner Summaries

## IAM

* **Users:** mapped to a physical user, has a password for AWS Console
* **Groups:** contains users only
* **Policies:** JSON document that outlines permissions for users or groups
* **Roles:** for EC2 instances or AWS services
* **Security:** MFA + Password Policy
* **Access Keys:** access AWS using the CLI or SDK
* **Audit**: IAM Credential Reports & IAM Access Advisor

## EC2

* **EC2 Instance:** AMI (OS) + Instance Size (CPU + RAM) + Storage + security groups + EC2 User Data
  * **Security Groups:** Firewall attached to the EC2 instance
  * **EC2 User Data:** Script launched at the first start of an instance
* **SSH**: start a terminal into our EC2 Instances (port 22)
* **EC2 Instance Role:** link to IAM roles
* **Purchasing Options:** On-Demand, Spot, Reserved (Standard + Convertible + Scheduled), Dedicated Host, Dedicated Instance

## EC2 Instance Storage

### EBS Volumes

* Network drives attached to one EC2 instance at a time
* Mapped to an Availability Zones
* Can use EBS Snapshots for backups / transferring EBS volumes across AZ

### AMI

* Create ready-to-use EC2 instances with our customizations

### EC2 Instance Store

* High performance hardware disk attached to our EC2 instance
* Lost if our instance is stopped / terminated

### EFS

* Network file system, can be attached to 100s of instances in a region

## ELB & ASG

* **High Availability** vs **Scalability** (vertical and horizontal) vs **Elasticity** vs **Agility** in the Cloud
* Elastic Load Balancers (ELB)
  * Distribute traffic across backend EC2 instances, can be Multi-AZ
  * Supports health checks
  *  3 types: **Application** LB (HTTP – L7), **Network** LB (TCP – L4), **Classic** LB (old)
* Auto Scaling Groups (ASG)
  * Implement Elasticity for your application, across multiple AZ
  * Scale EC2 instances based on the demand on your system, replace unhealthy
  * Integrated with the ELB

## S3

* **Buckets vs Objects**: global unique name, tied to a region
* **S3 security:** IAM policy, S3 Bucket Policy (public access), S3 Encryption
* **S3 Websites:** host a static website on Amazon S3
* **S3 Versioning:** multiple versions for files, prevent accidental deletes
* **S3 Access Logs:** log requests made within your S3 bucket
* **S3 Replication:** same-region or cross-region, must enable versioning
* **S3 Storage Classes:** Standard, IA, 1Z-IA, Intelligent, Glacier, Deep Archive
* **S3 Lifecycle Rules:** transition objects between classes
* **Snowball / Snowmobile:** import data onto S3 through a physical device
* **Storage Gateway:** hybrid solution to extend on-premises storage to S3

## Databases & Analytics

* **Relational Databases** - OLTP: RDS & Aurora (SQL)
* **In-memory Database:** ElastiCache
* **Key/Value Database:** DynamoDB (serverless)
* **Warehouse - OLAP:** Redshift (SQL)
* **Hadoop Cluster :** EMR
* **Athena:** query data on Amazon S3 (serverless & SQL)
* **Glue:** Managed ETL (Extract Transform Load) and Data Catalog service
* **Database Migration:** DMS

## Other Compute Services

* **Docker**: container technology to run applications
* **ECS**: run Docker containers on EC2 instances
* **Fargate**:
  * Run Docker containers without provisioning the infrastructure
  * Serverless offering (no EC2 instances)
* **ECR**: Private Docker Images Repository
* **Batch**: run batch jobs on AWS across managed EC2 instances
* **Lightsail**: predictable & low pricing for simple application & DB stacks

## Lambda

* Lambda is **Serverless, Function as a Service, seamless scaling, reactive**
* **Lambda Billing:**
  * By the time run x by the RAM provisioned
  * By the number of invocations
* **Language Support:** many programming languages except Docker
* **Invocation time:** up to 15 minutes
* **Use cases:**
  * Create Thumbnails for images uploaded onto S3
  * Run a Serverless cron job

## Deployment

* **CloudFormation: (AWS only)**
  * Infrastructure as Code, works with almost all of AWS resources
  * Repeat across Regions & Accounts
* **Beanstalk: (AWS only)**
  * Platform as a Service (PaaS), limited to certain programming languages or Docker
  * Deploy code consistently with a known architecture: ex, ALB + EC2 + RDS
* **CodeDeploy (hybrid):** deploy & upgrade any application onto servers
* **Systems Manager (hybrid):** patch, configure and run commands at scale
* **OpsWorks (hybrid):** managed Chef and Puppet in AWS

## Global Applications

* **Global DNS: Route 53**
  * Great to route users to the closest deployment with least latency
  * Great for disaster recovery strategies
* **Global Content Delivery Network (CDN): CloudFront**
  * Replicate part of your application to AWS Edge Locations – decrease latency
  * Cache common requests – improved user experience and decreased latency
* **S3 Transfer Acceleration**
  * Accelerate global uploads & downloads into Amazon S3
* **AWS Global Accelerator:**
  * Improve global application availability and performance using the AWS global network

## Cloud Integration

* SQS:
  * Queue service in AWS
  * Multiple Producers, messages are kept up to 14 days
  * Multiple Consumers share the read and delete messages when done
  * Used to decouple applications in AWS
* SNS:
  * Notification service in AWS
  * Subscribers: Email, Lambda, SQS, HTTP, Mobile…
  * Multiple Subscribers, send all messages to all of them
  * No message retention

## Monitoring

* **CloudWatch:**
  * **Metrics** : monitor the performance of AWS services and billing metrics
  * **Alarms** : automate notification, perform EC2 action, notify to SNS based on metric
  * **Logs** : collect log files from EC2 instances, servers, Lambda functions…
  * **Events** (or EventBridge): react to events in AWS, or trigger a rule on a schedule
* **CloudTrail** : audit API calls made within your AWS account
* **X-Ray**: trace requests made through your distributed applications
* **Service Health Dashboard:** status of all AWS services across all regions
* **Personal Health Dashboard**: AWS events that impact your infrastructure