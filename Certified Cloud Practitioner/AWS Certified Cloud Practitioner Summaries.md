# AWS Certified Cloud Practitioner Summaries

## Six Advantages of Cloud Computing

* Trade **capital expenses (CAPEX) for operational expenses/low variable costs**
* Benefit from **massive economies of scale**
* **Stop guessing capacity**
* Increase **speed and agility**
* Stop **spending money running and maintaining data centers**
* **Go global quickly**

## IAM

* **Users:** mapped to a physical user, has a password for AWS Console
* **Groups:** contains users only
* **Policies:** JSON document that outlines permissions for users or groups
* **Roles:** for EC2 instances or AWS services
* **Security:** MFA + Password Policy
  * **Virtual MFA device** - This is a software app that runs on a phone or other device and emulates a physical device.
  * **Hardware MFA device** - This is a hardware device that generates a six-digit numeric code based upon a time-synchronized one-time password algorithm.
  * **U2F security key** - Universal 2nd Factor (U2F) Security Key is a device that you can plug into a USB port on your computer.
* **Access Keys:** access AWS using the CLI or SDK
  * Access keys are long-term credentials **for an IAM user or the AWS account root user**.
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
* You can **dynamically change the configuration** of a volume attached to an instance

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
  * 3 types: 
    *  **Application** LB (HTTP – L7): This is best suited for **load balancing of HTTP and HTTPS traffic** and provides advanced request routing targeted at the delivery of modern application architectures, including microservices and containers.
    *  **Network** LB (TCP – L4): This is best suited for load balancing of Transmission Control Protocol (TCP), User Datagram Protocol (UDP) and Transport Layer Security (TLS) traffic where **extreme performance is required**
    *  **Classic** LB (old): This provides basic load balancing across multiple Amazon EC2 instances and operates at both the request level and connection level. 
* **Auto Scaling Groups (ASG)**
  * **Implement Elasticity for your application, across multiple AZ**
  * **Scale EC2 instances based on the demand on your system, replace unhealthy**
  * Integrated with the ELB

## S3

* **Buckets vs Objects**: global unique name, tied to a region
* **S3 security:** IAM policy, S3 Bucket Policy (public access), S3 Encryption
* **S3 Websites:** host a static website on Amazon S3
* **S3 Versioning:** multiple versions for files, prevent accidental deletes
* **S3 Access Logs:** log requests made within your S3 bucket
* **S3 Replication:** same-region or cross-region, must enable versioning
* **S3 Storage Classes:** 
  * **Standard**: Used for **frequently accessed data**
  * **IA**: Suitable for data that is **less frequently accessed, but requires rapid access** when needed
  * **1Z-IA**:  Storing secondary **backup copies of on-premise data** or storing **data you can recreate**
  * **Intelligent**: Cost-optimized by automatically **moving objects between two access tiers** based on changing access patterns
  * **Glacier and Glacier Deep Archive**: Low cost object storage (in GB/month) meant for archiving / backup
* **S3 Lifecycle Rules:** transition objects between classes
* **Snowball / Snowmobile:** import data onto S3 through a physical device
* **Storage Gateway:** hybrid cloud storage service that connects your existing on-premises environments with the AWS Cloud

## Databases & Analytics

* **Relational Databases**:
  * **RDS:** 
    * makes it easy to s**et up, operate, and scale** a relational database in the cloud.
    * It provides **cost-efficient and resizable capacity while automating time-consuming administration tasks** such as hardware provisioning, database setup, patching and backups.
  * **Aurora**: **MySQL and PostgreSQL-compatible** relational database
* **In-memory Database:** **ElastiCache:** With this service, you can build **data-intensive apps or improve the performance** of your existing apps by retrieving data from **high throughput and low latency in-memory data stores**
* **Key/Value Database:** **DynamoDB** (serverless) - **NoSQL**
* **Warehouse - OLAP:** Redshift (SQL)
* **Hadoop Cluster :** EMR
* **Athena:** query data on Amazon S3 (serverless & SQL)
* **Glue:** Managed ETL (Extract Transform Load) and Data Catalog service
* **Database Migration:** DMS

## Other Compute Services

* **Docker**: container technology to run applications
* **ECS**: run Docker containers on EC2 instances. **Servers can be managed.**
* **Fargate**:
  * Run Docker containers without provisioning the infrastructure
  * **Serverless** offering (no EC2 instances)
* **ECR**: Private Docker Images Repository (**Storage**)
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
  * **Infrastructure as Code**, works with almost all of AWS resources
  * Repeat across Regions & Accounts
* **Beanstalk: (AWS only)**
  * **Platform as a Service (PaaS)**, limited to certain programming languages or Docker
  * Deploy code consistently with a known architecture: ex, ALB + EC2 + RDS
* **CodeDeploy (hybrid):** deploy & upgrade any application onto servers
* **Systems Manager (hybrid):** patch, configure and run commands at scale
* **OpsWorks (hybrid):** managed Chef and Puppet in AWS

## Global Applications

* **Global DNS: Route 53**
  * Great to route users to the closest deployment with least latency
  * Great for disaster recovery strategies
  * Routing Policies:
    * **Weighted routing**: lets you associate multiple resources with a single domain name (example.com) or subdomain name (acme.example.com) and choose how much traffic is routed to each resource. 
    * **Failover routing policy** - This routing policy is used when you want to configure active-passive failover.
    * **Simple routing policy** - With simple routing, you typically route traffic to a single resource, for example, to a web server for your website.
    * **Latency routing policy** - This routing policy is used when you have resources in multiple AWS Regions and you want to route traffic to the region that provides the best latency.
* **Global Content Delivery Network (CDN): CloudFront**
  * Replicate part of your application to AWS Edge Locations – decrease latency
  * Cache common requests – improved user experience and decreased latency
* **S3 Transfer Acceleration**
  * Accelerate global uploads & downloads into Amazon S3
* **AWS Global Accelerator:**
  * Improve global application availability and performance using the AWS global network

## Cloud Integration

* **SQS:**
  * Queue service in AWS
  * Multiple Producers, messages are kept up to 14 days
  * Multiple Consumers share the read and delete messages when done
  * Used to decouple applications in AWS
* **SNS:**
  * Notification service in AWS
  * Subscribers: Email, Lambda, SQS, HTTP, Mobile…
  * Multiple Subscribers, send all messages to all of them
  * No message retention

## Monitoring

* **CloudWatch:**
  * **Metrics** : monitor the performance of AWS services and billing **metrics**
  * **Alarms** : automate notification, perform EC2 action, notify to SNS based on metric
  * **Logs** : collect log files from EC2 instances, servers, Lambda functions…
  * **Events** (or EventBridge): react to events in AWS, or trigger a rule on a schedule
* **CloudTrail** : audit API calls made within your AWS account
* **X-Ray**: 
  * **analyze and debug serverless and distributed applications** such as those built using a microservices architecture
  * identify and troubleshoot the root cause of performance issues and errors
* **Service Health Dashboard:** 
  * Status of all AWS services across all regions
  * Can be used to subscribe to an RSS feed to be notified of services' interruptions
* **Personal Health Dashboard**: AWS events that impact your infrastructure

## VPC

* **VPC - Virtual Private Cloud:** private network to deploy your resources (regional resource)
* **Subnets** allow you to partition your network inside your VPC (Availability Zone resource)
  * A **public subnet** is a subnet that is accessible from the internet
  * A **private subnet** is a subnet that is not accessible from the internet
  * To define access to the internet and between subnets, we use Route Tables
* **Internet Gateway:** at the VPC level, **provide Internet Access**
* **NAT Gateway / Instances:** **give internet access to private subnets**
* **NACL:** Stateless, subnet rules for inbound and outbound
* **Security Groups:** Stateful, operate at the EC2 instance level or ENI
* **VPC Peering:** **Connect two VPC with non overlapping IP** ranges, nontransitive
* **VPC Endpoints:** Provide **private access to AWS Services within VPC**
* **VPC Flow Logs:** network traffic logs
* **Site to Site VPN:** **VPN over public internet between on-premises DC and AWS**
* **Direct Connect:** direct **private connection to AWS**
* **Transit Gateway:** **Connect thousands of VPC and on-premises networks together**

## Security & Compliance

* **Shield**: Automatic DDoS Protection + 24/7 support for advanced
* **WAF**: Firewall to filter incoming requests based on rules
* **Penetration Testing**: No DDOS or zone walking
* **KMS**: **Encryption keys managed by AWS**
* **CloudHSM**: **Hardware** encryption, we manage encryption keys
* **Artifact**: Get access to compliance reports such as PCI, ISO, etc…
* **GuardDuty**: Find malicious behavior with VPC, DNS & CloudTrail Logs
* **Inspector**: For EC2 only, install agent and find vulnerabilities
* **Config**: Track config changes and compliance against rules
* **Macie**: Find sensitive data in Amazon S3 buckets
* **CloudTrail** : 
  * Track API calls made by users within account. 
  * Log, monitor and retain account activity related to actions across your AWS infrastructure

## Machine Learning

* **Rekognition**: face detection, labeling, celebrity recognition
* **Transcribe**: audio to text. **speech -> text**
* **Polly**: text to audio. **text -> speech**
* **Translate**: translations
* **Lex**: build conversational bots – **chatbots**
* **Connect**: cloud contact center
* **Comprehend**: natural language processing - **NLP**
* **SageMaker** : machine learning for every developer and data scientist

## Billing and Costing Tools

* **TCO Calculator:** To plan a move from **on-premises to AWS**
* **Simple Monthly Calculator / Pricing Calculator:** cost of services on AWS
* **Billing Dashboard:** high level overview + free tier dashboard
* **Cost Allocation Tags:** tag resources to create details on reports
* **Cost and Usage Reports:** 
  * Access **comprehensive** AWS cost and usage information
  * **Track your Amazon EC2 Reserved Instance (RI) usage**
  * **Leverage strategic data integrations**
* **Cost Explorer:** View **current usage (detailed)** and **forecast** usage
* **Billing Alarms:** in us-east-1 – track overall and per-service billing
* **Budgets:** **more advanced – track usage, costs, reserved instances, and get alerts**

## Account Best Practices
* Operate multiple accounts using **Organizations**
* Use **SCP** (service control policies) to restrict account power
* **Use Tags & Cost Allocation Tags** for easy management & billing
* **IAM guidelines:** MFA, least-privilege, password policy, password rotation
* **Config** to record all resources configurations & compliance over time
* **CloudFormation** to deploy stacks across accounts and regions
* **Trusted Advisor** to get insights
  * Trusted Advisor is an online tool that **provides real-time guidance to help provision your resources following AWS best practices**.
  * Checks in the following five categories:
    * **Cost Optimization** – recommendations that can potentially save you money by highlighting unused resources and opportunities to reduce your bill.
    * **Security** – identification of security settings that could make your AWS solution less secure.
    * **Fault Tolerance** – recommendations that help increase the resiliency of your AWS solution by highlighting redundancy shortfalls, current service limits, and over-utilized resources.
    * **Performance** – recommendations that can help to improve the speed and responsiveness of your applications.
    * **Service Limits** – recommendations that will tell you when service usage is more than 80% of the service limit.
* **Support Plan** adapted to your needs
  * **Basic**: A basic support plan is included for all AWS customers
  * **Developer**: Recommended if you are **experimenting or testing** in AWS.
  * **Business**: Recommended if you have **production workloads** in AWS.
  * **Enterprise**: Recommended if you have **business and/or mission critical workload**s in AWS.
* Send Service Logs and Access Logs to **S3 or CloudWatch Logs**
* **CloudTrail** to record API calls made within your account
* **If your Account is compromised:** change the root password, delete and rotate all passwords / keys, contact the AWS support

## Advanced Identity

* **IAM**
  * Identity and Access Management inside your AWS account
  * For users that you trust and belong to your company
* **Organizations**: manage multiple AWS accounts
  * AWS Organizations helps you to **centrally manage billing; control access, compliance, and security; and share resources across your AWS accounts.** 
  * **Consolidated billing**: 
    * **One bill**
    * **Easy tracking**
    * **Combined usage** – You can combine the usage across all accounts in the organization to share the volume pricing discounts and Reserved Instance discounts. 
    * **No extra fee**
* **Cognito**: create a database of users for your mobile & web applications
* **Directory Services**: integrate Microsoft Active Directory in AWS
* **Single Sign-On (SSO)**: one login for multiple AWS accounts & applications