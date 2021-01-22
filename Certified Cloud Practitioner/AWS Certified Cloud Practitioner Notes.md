# AWS Certified Cloud Practitioner Notes

* Notes derived from Stephane Maarek's AWS Certified Cloud Practitioner Slides

[TOC]

## How websites work

Client <----------> Network <----------> Server

* Clients and Servers have IP addresses

## What is a server composed of?

* **Compute**: CPU
* **Memory**: RAM
* **Storage**: Data
* **Database**: Store data in a structured way
* **Network**: Routers, switch, DNS server
  * **Network**: cables, routers and servers connected with each other
  * **Router**: A networking device that forwards data packets between computer networks. 
  * **Switch**: Takes a packet and send it to the correct server / client on your network

## Problems with traditional IT approach

* Pay for the rent for the data center
* Pay for power supply, cooling, maintenance
* Adding and replacing hardware takes time
* Scaling is limited
* Hire 24/7 team to monitor the infrastructure
* How to deal with disasters? (earthquake, power shutdown, fire…)

## Cloud Computing

* Cloud computing is the on-demand delivery of compute power, database storage,
  applications, and other IT resources
* Through a cloud services platform with pay-as-you-go pricing
* You can provision exactly the right type and size of computing resources you need
* You can access as many resources as you need, almost instantly
* Simple way to access servers, storage, databases and a set of application services

### The Deployment Models of the Cloud

**Private Cloud:**

* Cloud services used by a single organization, not exposed to the public.
* Complete control
* Security for sensitive applications
* Meet specific business needs

**Public Cloud**:

* Cloud resources owned and operated by a third-party cloud service provider delivered over the Internet
* **Six Advantages of Cloud Computing**:
  * Trade capital expenses for operational expenses
  * Benefit from massive economies of scale
  * Stop guessing capacity
  * Increase speed and agility
  * Stop spending money running and maintaining data centers
  * Go global quickly

**Hybrid Cloud**:

* Keep some servers on premises and extend some capabilities to the Cloud
* Control over sensitive assets in your private infrastructure
* Flexibility and cost-effectiveness of the public cloud

### The Five Characteristics of Cloud Computing

* On-demand self service
* Broad network access
* Multi-tenancy and resource pooling
* Rapid elasticity and scalability
* Measured service

### Problems solved by the Cloud

* **Flexibility**: change resource types when needed
* **Cost-Effectiveness**: pay as you go, for what you use
* **Scalability**: accommodate larger loads by making hardware stronger or adding additional nodes
* **Elasticity**: ability to scale out and scale-in when needed
* **High-availability and fault-tolerance**: build across data centers
* **Agility**: rapidly develop, test and launch software applications

### Types of Cloud Computing

**Infrastructure as a Service (IaaS)**

* Provide building blocks for cloud IT
* Provides networking, computers, data storage space
* Highest level of flexibility
* Easy parallel with traditional on-premises IT
* Only applications, data, runtime, middleware, and O/S on premises

**Platform as a Service (PaaS)**

* Removes the need for your organization to manage the underlying infrastructure
* Focus on the deployment and management of your applications
* Only applications and data on premises

**Software as a Service (SaaS)**

* Completed product that is run and managed by the service provider

### Pricing of the Cloud (AWS)

* **Compute**: Pay for compute time
* **Storage**: Pay for data stored
* **Data transfer**: Pay for data transfer OUT of the cloud. Into the cloud is free

## IAM

### Users and Groups

* IAM = Identity and Access Management
* A **global** service
* **Root account** created by default, and shouldn't be used or shared
* **Users** are people within your organization, and can be grouped
* **Groups** only contain users, not other groups

### Permissions

* Users or Groups can be assigned JSON documents called policies
* Policies define the permissions of the users
* **Least privilege principle**: Don't give more permission than a user needs

### Account Security

#### Password Policy

*  Strong passwords = higher security for your account
*  In AWS, you can setup a password policy:
  * Set a minimum password length
  * Require specific character types
  * Allow all IAM users to change their own passwords
  * Require users to change their password after some time (password expiration)
  * Prevent password re-use

#### Multi Factor Authentication - MFA

* MFA = password you know + security device you own
* Main benefit: If a password is stolen or hacked, the account is not compromised
* MFA Devices:
  * **Virtual MFA Device**:
    * Google Authenticator: Phone only
    * Authy: Multi-device
  * Universal 2nd Factor (U2F) Security Key
    * Physical Device
  * **Hardware Key Fob MFA Device**
  * **Hardware Key Fob MFA Device for AWS GovCloud**

#### How can users access AWS

* **AWS Management Console** (protected by password + MFA)
* **AWS Command Line Interface (CLI)**: protected by access keys
  * How to create access keys:
    * Use IAM User account
    * Go to security credentials and create access key
    * Save/Copy access keys and secret access key
    * When first using CLI: aws configure with access key, secret access key, and region code
    * aws iam list-user to get all users in account
* **AWS Software Developer Kit (SDK)** - for code: protected by access keys

### IAM Roles

* Some AWS service will need to perform actions on your behalf
* IAM roles are a secure way to grant permissions to entities that you trust. 

### IAM Security Tools

* **IAM Credentials Report** (account-level): In IAM menu
  * A report that lists all your account's users and the status of their various
    credentials
* **IAM Access Advisor** (user-level): A tab in the user's panel
  * Access advisor shows the service permissions granted to a user and when those services were last accessed.
  * Used to reduce privileges based on use

### IAM Guidelines and Best Practices

* Don’t use the root account except for AWS account setup
* One physical user = One AWS user
* Assign users to groups and assign permissions to groups
* Create a strong password policy
* Use and enforce the use of Multi Factor Authentication (MFA)
* Create and use Roles for giving permissions to AWS services
* Use Access Keys for Programmatic Access (CLI / SDK)
* Audit permissions of your account with the IAM Credentials Report

### Shared Responsibility Model for IAM

#### AWS Responsibilities

* Infrastructure
* Configuration and vulnerability analysis
* Compliance validation

#### Your Responsibilities

* Users, Groups, Roles, Policies management and monitoring
* Enable MFA on all accounts
* Rotate all your keys often
* Use IAM tools to apply appropriate permissions
* Analyze access patterns & review permissions

## EC2

*  EC2 = Elastic Compute Cloud = Infrastructure as a Service

### EC2 sizing and configuration

* AMI: 
  * You must use an AMI from the same region as that of the EC2 instance. 
  * The region of the AMI has no bearing on the performance of the EC2 instance

* Operating System ( OS ): Linux or Windows
* How much compute power & cores ( CPU )
* How much random-access memory ( RAM )
* How much storage space:
  * Network-attached ( EBS & EFS )
  * Hardware ( EC2 Instance Store )
* Network card: speed of the card, Public IP address
* Firewall rules: security group
* Bootstrap script (configure at first launch): EC2 User Data
* t2.micro is the free tier

### Security Groups

* They control how traffic is allowed into or out of our EC2 Instances.
* Security groups **only contain allow rules**
* Security groups rules **can reference by IP or by security group**
* Firewall on EC2 instances
* They regulate: 
  * Access to Ports
  * Authorized IP ranges – IPv4 and IPv6
  * Control of inbound network (from other to the instance)
  * Control of outbound network (from the instance to other)

### Classic Ports

* 22 = SSH (Secure Shell) - log into a Linux instance
* 21 = FTP (File Transport Protocol) – upload files into a file share
* 22 = SFTP (Secure File Transport Protocol) – upload files using SSH
* 80 = HTTP – access unsecured websites
* 443 = HTTPS – access secured websites
* 3389 = RDP (Remote Desktop Protocol) – log into a Windows instance

* Sources:
  * 0.0.0.0/0 = Everywhere on ipv4
  * ::/0 = Everywhere on ipv6
* Timeout caused by problems in security group rules

### SSH and EC2 Instance Connect

**Windows:** 

* Command Line or PowerShell
* Use command: ssh -i location\EC2Tutorial.pem ec2-user@public-ip-of-instance

**EC2 Instance Connect:**

* Go to instances
* Click on an instance and click connect
* Use EC2 Instance Connect

### EC2 IAM Roles

* Go to instance
* Right click to get security and go to modify IAM role
* Then add role defined in IAM
* Do not use aws configure in ssh/instance connect

### EC2 Instances Purchasing Options

#### On-Demand Instances

* short workload, predictable pricing
* Pay for what you use:
  * Linux - billing per second, after the first minute
  * All other operating systems (ex: Windows) - billing per hour
* Has the highest cost but no upfront payment
* No long-term commitment

#### Reserved: (MINIMUM 1 year)

* **Reserved Instances:** long workloads
  * Up to 72% discount compared to On-demand
  * Reservation period: **1 year = + discount | 3 years = +++ discount**
  * Purchasing options: **no upfront | partial upfront = + | All upfront = ++ discount**
  * Reserve a specific instance type
  * Recommended for **steady-state usage applications** (think database)
* **Convertible Reserved Instances:** long workloads with flexible instances
  * can change the EC2 instance type
  * Up to 45% discount
* **Scheduled Reserved Instances:** example – every Thursday between 3 and 6 pm
  * launch within time window you reserve
  * When you require a fraction of day / week / month
  * Commitment for 1 year only

* **Spot Instances**: short workloads, cheap, can lose instances (less reliable)
  * Can get a discount of up to 90% compared to On-demand
  * Instances that you can **“lose” at any point of time if your max price < current spot price**
  * The **MOST cost-efficient** instances in AWS
  * Useful for **workloads that are resilient to failure**
    * Batch jobs
    * Data analysis
    * Image processing
    * Any distributed workloads
    * Workloads with a flexible start and end time
  * **Not suitable for critical jobs or databases**
* **Dedicated Hosts**: book an entire physical server, control instance placement
  * Help address **compliance requirements**
  * Reduce costs by allowing you to **use your existing server-bound software licenses**
  * Allocated for your account for a 3-year period reservation
  * More expensive
  * Or for companies that have strong regulatory or compliance needs
* **Dedicated Instances**: no other customers will share your hardware
  * Instances running on hardware that’s dedicated to you
  * No control over instance placement (can move hardware after Stop / Start)

### Shared Responsibility Model for EC2

#### AWS Responsibilities

* Infrastructure
* Isolation on physical hosts
* Replacing faulty hardware
* Compliance validation

#### Your Responsibilities

* Security Groups rules
* Operating-system patches and updates
* Software and utilities installed on the EC2 instance
* IAM Roles assigned to EC2 & IAM user access management
* Data security on your instance

### EC2 Summary

* EC2 Instance: AMI (OS) + Instance Size (CPU + RAM) + Storage + security groups + EC2 User Data
* Security Groups: Firewall attached to the EC2 instance
* EC2 User Data: Script launched at the first start of an instance
* SSH: start a terminal into our EC2 Instances (port 22)
* EC2 Instance Role: link to IAM roles
* Purchasing Options: On-Demand, Spot, Reserved (Standard + Convertible + Scheduled), Dedicated Host, Dedicated Instance

## EC2 Instance Storage

### EBS

#### EBS Volume

* An **EBS (Elastic Block Store) Volume** is a **network** drive you can attach
  to your instances while they run
  * It uses the network to communicate the instance, which means there might be a bit of latency
  *  It can be detached from an EC2 instance and attached to another one quickly
* It allows your instances to persist data, even after their termination
* **They can only be mounted to one instance at a time** (at the CCP level)
*  They are bound to a specific availability zone
  * An EBS Volume in us-east-1a cannot be attached to us-east-1b
* Have a provisioned capacity (size in GBs, and IOPS)
  * You get billed for all the provisioned capacity
  * You can increase the capacity of the drive over time

#### EBS Snapshots

* Make a backup (snapshot) of your EBS volume at a point in time
* Not necessary to detach volume to do snapshot, but recommended
* Can copy snapshots across AZ or Region

### AMI

* AMI = Amazon Machine Image
* AMI are a customization of an EC2 instance
  * You add your own software, configuration, operating system, monitoring
  * Faster boot / configuration time because all your software is pre-packaged
* AMI are built for a specific region
* You can launch EC2 instances from:
  * A Public AMI: AWS provided
  * Your own AMI: you make and maintain them yourself
  * An AWS Marketplace AMI: an AMI someone else made (and potentially sells)

### EC2 Instance Store

* EBS volumes are network drives with good but “limited” performance
* **If you need a high-performance hardware disk, use EC2 Instance Store**
* Better I/O performance
* EC2 Instance Store lose their storage if they’re stopped (ephemeral)
  * Good for buffer / cache / scratch data / temporary content
* Risk of data loss if hardware fails

### EFS

* EFS – Elastic File System
* **Managed NFS (network file system) that can be mounted on 100s of EC2**
* EFS works with Linux EC2 instances in multi-AZ
* **Highly available, scalable, expensive (3x gp2), pay per use, no capacity planning**

### Shared Responsibility Model for EC2 Storage

#### AWS Responsibilities

* Infrastructure
* Replication for data for EBS Volumes and EFS drives
* Replacing faulty hardware
* Ensuring their employees cannot access your data

#### Your Responsibilities

* Setting up backup / snapshot procedures
* Setting up data encryption
* Responsibility of any data on the drives
* Understanding the risk of using EC2 Instance Store

## Elastic Load Balancing & Auto Scaling Groups
* **Scalability**: ability to accommodate a larger load by making the hardware stronger (scale up), or by adding nodes (scale out)
* **Elasticity**: once a system is scalable, elasticity means that there will be some “auto-scaling” so that the system can scale based on the load. This is “cloud-friendly”: pay-per-use, match demand, optimize costs
* **Agility**: (not related to scalability - distractor) new IT resources are only a click away, which means that you reduce the time to make those resources available to your developers from weeks to just minutes.
* There are two kinds of scalability:
  * Vertical Scalability
  * Horizontal Scalability (= elasticity)
* Scalability is linked but different to High Availability

### Vertical Scalability

* Means increasing the size of the instance
* ex. t2.micro -> t2.large
* Vertical scalability is very common for non distributed systems, such as a database.
* There is a hardware limit

### Horizontal Scalability

* Means increasing the number of instances / systems for your application
* This is very common for web applications / modern applications

### High Availability

* Means running your application / system in at least 2 Availability Zones
* The goal of high availability is to survive a data center loss (disaster)

### Load Balancing

* Load balancers are **servers that forward internet traffic to multiple servers** (EC2 Instances) downstream.
* **Why use a load balancer?**
  * Spread load across multiple downstream instances
  * Expose a single point of access (DNS) to your application
  * Seamlessly handle failures of downstream instances
  * Do regular health checks to your instances
  * Provide SSL termination (HTTPS) for your websites
  * High availability across zones
* An **ELB (Elastic Load Balancer)** is a managed load balancer
  * AWS guarantees that it will be working
  * AWS takes care of upgrades, maintenance, high availability
  * AWS provides only a few configuration knobs
  * Costs less to maintain your own load balancer but requires of maintenance and integrations
  * **3 kinds of load balancers offered by AWS:**
    * **Application Load Balancer** (**HTTP / HTTPS only**) – Layer 7
    * **Network Load Balancer** (**ultra-high performance**, allows for TCP) – Layer 4
    * **Classic Load Balancer** (slowly retiring) – Layer 4 & 7

### Auto Scaling Group

*  In real-life, the load on your websites and application can change
*  In the cloud, you can create and get rid of servers very quickly
* The goal of an Auto Scaling Group (ASG) is to:
  * Scale out (add EC2 instances) to match an increased load and Scale (remove EC2 instances) to match a decreased load
  * Ensure we have a minimum and a maximum number of machines running
  * Automatically register new instances to a load balancer
  * Replace unhealthy instances
* **Cost Savings:** only run at an optimal capacity 

## S3

* Global Service
* Backup and storage
* Disaster Recovery
* Archive
* Hybrid Cloud storage
* Application/Media hosting
* Data lakes & big data analytics
* Software delivery
* Static website

### Buckets

* Amazon S3 allows people to store objects (files) in “buckets” (directories)
* Buckets must have a globally unique name (across all regions all accounts)
* Buckets are defined at the **region level**

### Objects

* Objects (files) have a Key
* The key is the FULL path:
* The key is composed of prefix + object name
* Object values are the content of the body:
  * Max Object Size is 5TB (5000GB)
  * If uploading more than 5GB, must use “multi-part upload”
* Metadata (list of text key / value pairs – system or user metadata)
* Tags
* Version ID

### Security

* **User based**
  * IAM policies - which API calls should be allowed for a specific user from IAM console
* **Resource Based**
  * Bucket Policies - bucket wide rules from the S3 console - allows cross account
  * Object Access Control List (ACL) – finer grain
  * Bucket Access Control List (ACL) – less common
* **Note: an IAM principal can access an S3 object if**
  * the user IAM permissions allow it OR the resource policy ALLOWS it
  * AND there’s no explicit DENY
* **Encryption**: encrypt objects in Amazon S3 using encryption keys

#### S3 Bucket Policies

* JSON based policies
  * Resources: buckets and objects
  * Actions: Set of API to Allow or Deny
  * Effect: Allow / Deny
  * Principal: The account or user to apply the policy to
* Grant public access to the bucket
  * Default access is blocked to prevent company data leaks
  * Block public access settings at the account level
* Force objects to be encrypted at upload
* Grant access to another account 

### S3 Websites and Versioning

* Websites:
  * S3 can host static websites and have them accessible on the www
  * Website needs to be publicly accessible via bucket policy
* Versioning is enabled at the bucket level:
  * Protect against unintended deletes (ability to restore a version)
  * Easy roll back to previous version

### S3 Access Logs

* For audit purpose, you may want to log all access to S3 buckets
* Any request made to S3, from any account, authorized or denied, will be logged into another S3 bucket

### S3 Replication (CRR & SRR)

* Cross Region Replication (CRR):
  * compliance, lower latency access, replication across accounts
* Same Region Replication (SRR)
  * log aggregation, live replication between production and test accounts
* Must enable versioning in source and destination

### S3 Storage Classes

* Durability: How often you lose a file
  * High durability (99.999999999%, 11 9’s) of objects across multiple AZ
* Availability: Measures how readily available a service is
  * S3 standard has 99.99% availability, which means it will not be available 53 minutes a year

#### Amazon S3 Standard - General Purpose

* **Availability**: 99.99%
* Used for frequently accessed data
* Low latency and high throughput
* **Use Cases**: Big Data analytics, mobile & gaming applications, content distribution

#### Amazon S3 Standard-Infrequent Access (IA)

* Suitable for data that is less frequently accessed, but requires rapid access when needed

* **Availability**: 99.9%
* Lower cost compared to Amazon S3 Standard, but retrieval fee
* **Use Cases**: As a data store for disaster recovery, backups

#### S3 Intelligent-Tiering

* **Availability**: 99.9%
* Same low latency and high throughput performance of S3 Standard
* **Cost-optimized by automatically moving objects between two access tiers** based on changing access patterns:
  * Frequent access
  * Infrequent access
*  Resilient against events that impact an entire Availability Zone

#### Amazon S3 One Zone-Infrequent Access

* **Availability**: 99.5%
* Low latency and high throughput performance
* Lower cost compared to S3-IA (by 20%)
* **Use Cases:** Storing secondary backup copies of on-premise data, or storing data you can recreate

#### Amazon Glacier and Amazon Glacier Deep Archive

* Low cost object storage (in GB/month) meant for archiving / backup
* Data is retained for the longer term (years)
* Amazon Glacier - Cheap:
  * Expedited (1 to 5 minutes)
  * Standard (3 to 5 hours)
  * Bulk (5 to 12 hours)
* Amazon Glacier Deep Archive – Cheapest:
  * Standard (12 hours)
  * Bulk (48 hours)

### Shared Responsibility Model for S3

#### AWS Responsibilities

* Infrastructure (global security, durability, availability, sustain concurrent loss of data in
  two facilities)
* Configuration and vulnerability analysis
* Compliance validation

#### Your Responsibilities

* S3 Versioning
* S3 Bucket Policies
* S3 Replication Setup
* Logging and Monitoring
* S3 Storage Classes
* Data encryption at rest and in transit

## Snowball

* **Physical data transport solution** that helps moving TBs or PBs of data in or out of AWS
* Alternative to moving data over the network (and paying network fees)
* Pay per data transfer job
* Use cases: large data cloud migrations, DC decommission, disaster recovery
* **If it takes more than a week to transfer over the network, use Snowball devices**

### Snowball Process

1. Request snowball devices from the AWS console for delivery
2. Install the snowball client on your servers
3. Connect the snowball to your servers and copy files using the client
4. Ship back the device when you’re done (goes to the right AWS facility)
5. Data will be loaded into an S3 bucket
6. Snowball is completely wiped

### Snowball Edge

* Snowball Edges (100 TB) add computational capability to the device
* Supports EC2 AMI and Lambda functions
* Supports custom Lambda functions
* Use case: data migration, image collation, IoT capture, machine learning

### AWS Snowmobile

* Transfer exabytes of data (1 EB = 1,000 PB = 1,000,000 TBs)
* **Better than Snowball if you transfer more than 10 PB**

### Hybrid Cloud for Storage

* AWS is pushing for ”hybrid cloud”
  * Mix of on premises and on the cloud infrastructure
* This can be due to:
  *  Long cloud migrations
  *  Security requirements
  *  Compliance requirements
  *  IT strategy

#### AWS Storage Gateway

* Bridge between on-premise data and cloud data in S3
* **Hybrid storage service to allow on-premises to seamlessly use the AWS Cloud**

## Databases

* You can structure the data
* You build indexes to efficiently query / search through the data
* You define relationships between your datasets
* Databases are optimized for a purpose and come with different features, shapes and constraints

### Relational Databases

* Can use the SQL language to perform queries / lookups

### NoSQL Databases

* NoSQL = non-SQL = non relational databases
* Benefits:
  * **Flexibility**: easy to evolve data model
  * **Scalability**: designed to scale-out by using distributed clusters
  * **High-performance**: optimized for a specific data model
  * **Highly functional:** types optimized for the data model
* **Examples**: Key-value, document, graph, in-memory, search databases

### Databases & Shared Responsibility on AWS

* AWS offers use to manage different databases
* Benefits include:
  * Quick Provisioning, High Availability, Vertical and Horizontal Scaling
  * Automated Backup & Restore, Operations, Upgrades
  * Operating System Patching is handled by AWS
  * Monitoring, alerting

### RDS

* RDS stands for Relational Database Service
* It’s a managed DB service for DB use SQL as a query language.

#### Advantage over using RDS versus deploying DB on EC2

* RDS is a managed service:
* Automated provisioning, OS patching
* Continuous backups and restore to specific timestamp (Point in Time Restore)!
* Monitoring dashboards
* Read replicas for improved read performance
* Multi AZ setup for DR (Disaster Recovery)
* Maintenance windows for upgrades
* Scaling capability (vertical and horizontal)
* Storage backed by EBS (gp2 or io1)
* **CANNOT** SSH into your instances

### Aurora

* PostgreSQL and MySQL are both supported as Aurora DB
* 5x performance improvement over MySQL on RDS, over 3x the performance of Postgres on RDS
* Aurora storage automatically grows in increments of 10GB, up to 64 TB.
*  Aurora costs more than RDS (20% more) – but is more efficient

### ElastiCache

* ElastiCache is to get managed Redis or Memcached
* Caches are **in-memory databases** with high performance, low latency
* Helps **reduce load off databases for read intensive workloads**

### DynamoDB

* Fully Managed Highly available with replication across 3 AZ
* **NoSQL database - not a relational database**
* Scales to massive workloads, distributed “ serverless ” database
* Fast and consistent in performance
* **Single-digit millisecond latency-low latency retrieval**
* Low cost and auto scaling capabilities
* DynamoDB is a key/value database

### Redshift

* Redshift is based on PostgreSQL, but it’s **not used for OLTP**
* It’s OLAP – **online analytical processing (analytics and data warehousing)**
* Load data once every hour, not every second
* 10x better performance than other data warehouses, scale to PBs of data
* **Columnar** storage of data (instead of row based)
* Pay as you go based on the instances provisioned
* BI tools such as AWS Quicksight or Tableau integrate with it

### Amazon EMR

* EMR stands for “Elastic MapReduce”
* EMR helps creating **Hadoop clusters (Big Data)** to analyze and process vast amount of data
* The clusters can be made of **hundreds of EC2 instances**
* **Use cases: data processing, machine learning, web indexing, big data**

### Athena

* Fully Serverless database with SQL capabilities
* Used to query data in S3
* **Use Case: one-time SQL queries, serverless queries on S3, log analytics**

### Glue

* **Managed extract, transform, and load (ETL) service**
* Useful to prepare and transform data for analytics

### DMS – Database Migration Service

* Quickly and securely migrate databases to AWS, resilient, self healing
* The source database remains available during the migration
* Supports Migrations:
  * Homogenous: ex Oracle to Oracle
  * Heterogenous: ex Microsoft SQL Server to Aurora

### Deployment

* **Multi-AZ:** 
  * **High Availability**
  * Spans at least 2 AZ in one region
* **Multi-Region:**
  * **Disaster Recovery and Local Performance**
  * Each region can have Multi-AZ deployment
* **Read Replica:** 
  * **Scalability**
  * Can be within an AZ, Cross-AZ or Cross Region

## Other Compute Services

### Docker

* Docker is a software development platform to deploy apps
* Apps are packaged in **containers** that can be run on any OS
* **Apps run the same, regardless of where they’re run**
* Scale containers up and down very quickly (seconds)

#### Images

* Docker images are stored in Docker Repositories
* Public: Docker Hub https://hub.docker.com/
* Private: Amazon ECR

#### ECS (Server)

* ECS = Elastic Container Service
* **Launch Docker containers on AWS**
* **Your Responsibilities:** must provision & maintain the infrastructure (the EC2 instances)
* **AWS Responsibilities:** takes care of starting / stopping containers

#### Fargate (Serverless)

* **Launch Docker containers on AWS**
* **Your Responsibilities:** You do not provision the infrastructure (no EC2 instances to manage)
* **AWS Responsibilities:** Runs containers for you based on the CPU / RAM you need
* **Serverless offering**

#### ECR (Storage)

* Elastic Container Registry
* Private Docker Registry
* **This is where you store your Docker images**

### Lambda

* **Serverless**:
  * A new paradigm in which the developers don’t have to manage servers anymore
  * It means that you don't manage / provision / see servers
  * ex. S3, DynamoDB, Fargate, Lambda
* Virtual functions
* Short executions
* Run on- - demand
* Scaling is automated 

#### Benefits

* Easy Pricing:
  * **Pay per call/Pay per duration**
  * Free tier of 1,000,000 AWS Lambda requests and 400,000 GBs of compute time
* Integrated with the whole AWS suite of services
* Event-Driven: functions get invoked by AWS when needed
* Easy to get more resources per functions
* Increasing RAM will also improve CPU and network

### Batch

* **Fully managed batch processing at any scale**
* Efficiently run 100,000s of computing batch jobs on AWS
* **A “batch” job is a job with a start and an end (opposed to continuous)**
* **Batch will dynamically launch EC2 instances or Spot Instances**
* Batch jobs are defined as Docker images and run on ECS
* Helpful for cost optimizations and focusing less on the infrastructure

### Batch vs Lambda
* Lambda:
  * Time limit
  * Limited runtimes
  * Limited temporary disk space
  * Serverless
* Batch:
  * No time limit
  * Any runtime as long as it’s packaged as a Docker image
  * Rely on EBS / instance store for disk space
  * Relies on EC2 (can be managed by AWS)

### Lightsail

* Virtual servers, storage, databases, and networking
* **Low & predictable pricing**
* **Great for people with little cloud experience**
* Use cases: 
  * Simple web applications (has templates for LAMP, Nginx, MEAN, Node.js…)
  * Websites (templates for WordPress, Magento, Plesk, Joomla)
  * Dev / Test environment
* Has high availability but no auto-scaling, limited AWS integrations

## Deploying and Managing Infrastructure at Scale 
### CloudFormation

* CloudFormation allows you to use **programming languages or a simple text file to model and provision, in an automated and secure manner, all the resources needed for your applications across all Regions and accounts.**
* CloudFormation creates configuration in the **right order and exactly how you specify**
* Used we need to repeat an architecture in different environments/regions/AWS accounts
* Benefits 
  * **Infrastructure as code**:
    * No resources are manually created, which is excellent for control
    * Changes to the infrastructure are reviewed through code
  * **Cost:** 
    * Each resources within the stack is tagged with an identifier so you can easily see how much a stack costs you
    * You can estimate the costs of your resources using the CloudFormation template
  * **Productivity:**
    * Ability to destroy and re-create an infrastructure on the cloud on the fly
    * Automated generation of Diagram for your templates
  * **Supports (almost) all AWS resources**

### Elastic Beanstalk

* Elastic Beanstalk an easy-to-use service for deploying and scaling web applications and services. 
* **Beanstalk = Platform as a Service (PaaS)**
  * Managed service
    * Instance configuration / OS is handled by Beanstalk
    * Deployment strategy is configurable but performed by Elastic Beanstalk
  * **Just the application code is the responsibility of the developer**
  * Three architecture models:
    *  Single Instance deployment: good for dev
    * LB + ASG: great for production or pre-production web applications
    * ASG only: great for non-web apps in production (workers, etc..)
* Beanstalk is free but you pay for the underlying instances

### CodeDeploy

* **We want to deploy our application automatically**
* Works with **EC2 Instances**
* Works with **On-Premises Servers**
* Works with **serverless Lambda functions**
* **Hybrid service**
* Helps in upgrading versions

### Systems Manager (SSM)

* **Helps you manage your EC2 and On-Premises systems at scale**
* **Another Hybrid AWS service**
* **Get operational insights about the state of your infrastructure**
* **Most important features are:**
  * **Patching automation for enhanced compliance**
  * **Run commands across an entire fleet of servers**
  * Store parameter configuration with the SSM Parameter Store

### OpsWorks

* Chef & Puppet help you perform server configuration automatically, or repetitive actions
* Only provision standard AWS resources 

## Global Infrastructure

* A **global application** is an application deployed in **multiple geographies**
* On AWS: this could be Regions and / or Edge Locations
* **Decreased Latency**
* **Disaster Recovery (DR)**
* **Attack protection**

### Route 53

* Great to route users to the closest deployment with least latency
* Great for disaster recovery strategies
* **Route53 is a Managed DNS (Domain Name System)**
  * DNS is a collection of rules and records which helps clients understand how to reach a server through URLs.
* Records:
  * A record (IPv4 mapping)
  * AAAA (IPv6 mapping)
  * CNAME (hostname to hostname)
  * Alias (ELB, CloudFront, S3, RDS, etc … mapping)
* Routing Policies:
  * **Simple Routing Policy**: NO health checks)
  * **Weighted Routing Policy**: Use health checks to distribute loads
  * **Latent Routing Policy**: Redirection to closest server
  * **Failover Routing Policy**: Redirection based on health of an instance

### AWS CloudFront

* Content Delivery Network (CDN)
* **Improves read performance, content is cached at the edge**
* **DDoS protection** (because worldwide), integration with Shield, AWS Web Application Firewall
* CloudFront can cache from:
  * **S3 bucket**
    * For distributing files and caching them at the edge
    * Enhanced security with CloudFront **Origin Access Identity (OAI)**
    * CloudFront can be used as an ingress (to upload files to S3)
  * **Custom Origin (HTTP**)
    * Application Load Balancer
    * EC2 instance
    * S3 website (must first enable the bucket as a static S3 website)
    * Any HTTP backend you want

#### CloudFront vs S3 Cross Region Replication

* CloudFront:
  * Global Edge network
  * Files are cached for a TTL (maybe a day)
  * **Great for static content that must be available everywhere**

* S3 Cross Region Replication:
  * Must be setup for each region you want replication to happen
  * Files are updated in near real-time
  * Read only
  * **Great for dynamic content that needs to be available at low-latency in few regions**

### S3 Transfer Acceleration

* Increase transfer speed by transferring file to an AWS edge location which will forward the data to the S3 bucket in the target region

### AWS Global Accelerator

* **Improve global application availability and performance using the AWS global network**
* Leverage the AWS internal network to optimize the route to your application (60% improvement)
* **2 Anycast IP are created for your application and traffic is sent through Edge Locations**

### AWS Global Accelerator vs CloudFront

* They both use the AWS global network and its edge locations
* Both services integrate with AWS Shield for DDoS protection.
* CloudFront - Content Delivery Network
  * Improves performance for your cacheable content (such as images and videos)
  * Content is served at the edge
* Global Accelerator
  * No caching, proxying packets at the edge to applications running in one or more AWS Regions.
  * Improves performance for a wide range of applications over TCP or UDP
  * Good for HTTP use cases that require static IP addresses
  * Good for HTTP use cases that required deterministic, fast regional failover

## Cloud Integration

* 2 patterns of application communication
  * **Synchronous communications (application to application)**
  * **Asynchronous / Event based (application to queue to application)**

### SQS

* Fully managed service (~serverless), use to **decouple** applications
* **Messages are deleted after they’re read by consumers**
* **Consumers share the work to read messages & scale horizontally**

### SNS

* One message to many receivers
* The **“event publishers ”** only sends message to one SNS topic
* The **“event publishers ”** only sends message to one SNS topic
* As many “event subscribers ” as we want to listen to the SNS topic notifications

## Cloud Monitoring

### CloudWatch Metrics

* provides metrics for every services in AWS
* Metric is a variable to monitor (CPUUtilization, NetworkIn…)
* Metrics have timestamps
* Important Metrics:
  * **EC2 instances:** CPU Utilization, Status Checks, Network (not RAM)
  * **EBS volumes:** Disk Read/Writes
  * **S3 buckets:** BucketSizeBytes, NumberOfObjects, AllRequests
  * **Billing:** Total Estimated Charge (only in us-east-1)
  * **Service Limits:** how much you’ve been using a service API
  * **Custom metrics**
* Alarms: Are used to trigger notifications for any metric

#### Logs

* Collects logs from different AWS applications
* Enables real-time monitoring of logs
* CloudWatch Logs for EC2:
  * You need to run a CloudWatch agent on EC2 to push the log files you want
  * The CloudWatch log agent can be setup on-premises too

#### Events

* Schedule: Cron jobs (scheduled scripts)
* Event Pattern: Event rules to react to a service doing something
* Trigger Lambda functions, send SQS/SNS messages

#### EventBridge

* **Default event bus:** generated by AWS services (CloudWatch Events)
* **Partner event bus:** receive events from SaaS service or applications (Zendesk, DataDog, Segment, Auth0…)
* **Custom Event buses:** for your own applications
* **Schema Registry:** model event schema

### CloudTrail

* Provides governance, compliance and audit for your AWS Account
* Get an history of events / API calls made within your AWS Account
* A trail can be applied to All Regions (default) or a single Region.

### X-ray

* Troubleshooting performance (bottlenecks)
* Understand dependencies in a microservice architecture
* Pinpoint service issues
* Review request behavior
* Find errors and exceptions

### Service Health Dashboard

* **AWS Personal Health Dashboard provides** **alerts and remediation guidance when AWS is experiencing events that may impact you** 
* Personal Health Dashboard gives you a personalized view into the performance and availability of the AWS services underlying your AWS resources.

## VPC

* **VPC - Virtual Private Cloud:** private network to deploy your resources (regional resource)
* **Subnets** allow you to partition your network inside your VPC (Availability Zone resource)
  * A **public subnet** is a subnet that is accessible from the internet
  * A **private subnet** is a subnet that is not accessible from the internet
  * To define access to the internet and between subnets, we use Route Tables
* **Internet Gateway:** at the VPC level, provide Internet Access
* **NAT Gateway / Instances:** give internet access to private subnets
* **NACL:** Stateless, subnet rules for inbound and outbound
* **Security Groups:** Stateful, operate at the EC2 instance level or ENI
* **VPC Peering:** Connect two VPC with non overlapping IP ranges, nontransitive
* **VPC Endpoints:** Provide private access to AWS Services within VPC
* **VPC Flow Logs:** network traffic logs
* **Site to Site VPN:** VPN over public internet between on-premises DC and AWS
* **Direct Connect:** direct private connection to AWS
* **Transit Gateway:** Connect thousands of VPC and on-premises networks together

## Security and Compliance

### AWS Shared Responsibility Model

* **AWS Responsibility - Security of the Cloud**
  * Protecting infrastructure (hardware, software, facilities, and networking) that runs all the AWS services
  * Managed services like S3, DynamoDB, RDS, etc.
* **Customer responsibility - Security in in the Cloud**
  * For EC2 instance, customer is responsible for management of the guest OS (including security patches and updates), firewall & network configuration, IAM
  * Encrypting application data
* **Shared controls:**
  * Patch Management, Configuration Management, Awareness & Training

### DDOS Protection

#### AWS Shield

* **Standard**
  * Free service that is activated for every AWS customer
  * Provides protection from attacks such as SYN/UDP Floods, Reflection attacks
    and other layer 3/layer 4 attacks
* **Advanced:**
  * Optional DDoS mitigation service ($3,000 per month per organization)
  * Protect against more sophisticated attack on Amazon EC2, Elastic Load Balancing (ELB), Amazon CloudFront, AWS Global Accelerator, and Route 53
  *  24/7 access to AWS DDoS response team (DRP)

#### WAF

* Protects your web applications from common web exploits (Layer 7)
* Layer 7 is HTTP (vs Layer 4 is TCP)
* Deploy on Application Load Balancer , API Gateway, CloudFront

### Penetration Testing

* Self test on their on AWS infrastructure without prior approval for 8 services
* Prohibited Activities
  * DNS zone walking via Amazon Route 53 Hosted Zones
  * Denial of Service (DoS), Distributed Denial of Service (DDoS), Simulated DoS, Simulated DDoS
  * Port flooding
  * Protocol flooding
  * Request flooding (login request flooding, API request flooding)

### KMS (Key Management Service)

* KMS = AWS manages the encryption keys
* Some services require **Encryption to be Opt-in:**
* **Encryption Automatically enabled:**
  * **CloudTrail Logs**
  * **S3 Glacier**
  * **Storage Gateway**
* **Key Types:**
  * **Customer Manager CMK:**
    * Create, manage and use, can enable or disable
    * Possibility of rotation policy (new key generated every year, old key preserved)
    * Possibility to bring-your-own-key
  * **AWS managed CMK:**
    * Used by AWS service (aws/s3, aws/ebs, aws/redshift)
  * **CloudHSM Keys (custom keystore):**
    *  Keys generated from your own CloudHSM hardware device
    * Cryptographic operations are performed within the CloudHSM cluster

### CloudHSM

* CloudHSM => AWS provisions encryption hardware
* You manage your own encryption keys entirely (not AWS)

### Secrets Manager

* Newer service, meant for storing secrets
* Capability to force rotation of secrets every X days
* Integration with Amazon RDS (MySQL, PostgreSQL, Aurora)

### Artifact

* Portal that provides customers with on-demand access to AWS **compliance documentation** and AWS agreements
* **Can be used to support internal audit or compliance**

### GuardDuty

* Intelligent Threat discovery to Protect AWS Account
* Uses Machine Learning algorithms, anomaly detection, 3rd party data

### Inspector

* Automated Security Assessments for EC2 instances
* Analyze against unintended network accessibility

### Config

* **Helps with auditing and recording compliance of your AWS resources**
* **Helps record configurations and changes over time**
* AWS Config is a per-region service
* Resource:
  * View compliance of a resource over time
  * View configuration of a resource over time
  * View CloudTrail API calls if enabled

### Macie

* Amazon Macie is a fully managed data security and data privacy service that uses **machine learning and pattern matching to discover and protect your sensitive data in AWS.**
* Macie helps identify and alert you to **sensitive data, such as personally identifiable information (PII)**

## Machine Learning

### Rekognition

* Find **objects, people, text, scenes in images and videos** using ML
* **Facial analysis** and **facial search** to do user verification, people counting

### Transcribe

* Automatically **convert speech to text**
* Uses a **deep learning process** called automatic speech recognition (ASR) to convert speech to text quickly and accurately

### Polly

* Turn **text into lifelike speech** using deep learning

### Translate

* Natural and accurate language translation
* Amazon Translate allows you to localize content

### Lex

* Natural Language Understanding to recognize the intent of text, callers
* Helps build chatbots, call center bots

### Connect

* Receive calls, create contact flows, cloud-based virtual contact center
* Can integrate with other CRM systems or AWS

### Comprehend

* For Natural Language Processing – NLP
* Uses machine learning to find insights and relationships in text

### SageMaker

* Fully managed service for developers / data scientists to build ML models
* Typically difficult to do all the processes in one place + provision servers

## Account Management, Billing & Support
### Organizations

* Global service
* Allows to manage **multiple AWS accounts**
* The main account is the master account
* Cost Benefits:
  * **Consolidated Billing** across all accounts - single payment method
  * Pricing benefits from **aggregated usage** (volume discount for EC2, S3…)
  * **Pooling of Reserved EC2** instances for optimal savings
* API is available to **automate AWS account creation**
* **Restrict account privileges using Service Control Policies (SCP)**

* Create accounts per **department** , per **cost center**, per **dev / test / prod** , based on **regulatory restrictions** (using SCP), for **better resource isolation** (ex: VPC), to have **separate per-account service limits** , isolated account for **logging**

### Pricing Models

* AWS has 4 pricing models:
* **Pay as you go:** pay for what you use, remain agile, responsive, meet scale demands
* **Save when you reserve:** minimize risks, predictably manage budgets, comply with long-terms requirements
  * Reservations are available for EC2 Reserved Instances, DynamoDB Reserved
    Capacity, ElastiCache Reserved Nodes, RDS Reserved Instance, Redshift Reserved
    Nodes
* **Pay less by using more:** volume-based discounts
* **Pay less as AWS grows**

### Billing and Costing Tools

* **Estimating costs in the cloud:**
  * TCO Calculator
  * Simple Monthly Calculator / Pricing Calculator
* **Tracking costs in the cloud:**
  * Billing Dashboard
  * Cost Allocation Tags
  * Cost and Usage Reports
  * Cost Explorer
* **Monitoring against costs plans:**
  * Billing Alarms
  * Budgets

### TCO

* AWS helps you reduce Total Cost of Ownership (TCO) by r**educing the need to invest in large capital expenditures** and providing a **pay-as-you-go model**
* The TCO calculators allow you to **estimate the cost savings** when using AWS and provide a detailed set of reports that can be used in **executive presentations.**

### Tracking Costs

#### Cost Allocation Tags

* Use **cost allocation tags** to track your AWS costs on a detailed level
* **AWS generated tags** and **User-defined tags**

#### Cost and Usage Reports

* The AWS Cost & Usage Report contains the most comprehensive set of AWS cost and usage data available , including additional metadata about AWS services, pricing, and reservations (e.g., Amazon EC2 Reserved Instances (RIs)).

#### Cost Explorer (Forecast)

* Visualize, understand, and manage your AWS costs and usage over time
* Analyze your data at a high level: total costs and usage across all accounts
* **Forecast usage up to 3 months based on previous usage**

### Monitoring Against Costs

#### Billing Alarms in CloudWatch

* Billing data metric is stored in CloudWatch us-east-1
* Billing data are for overall worldwide AWS costs

#### AWS Budgets

* Create budget and send alarms when costs exceeds the budget
* 3 types of budgets: Usage, Cost, Reservation

### Trusted Advisor

* Analyze your AWS accounts and provides recommendation
* Full Trusted Advisor – Available for **Business & Enterprise support plans**
  * Ability to set CloudWatch alarms when reaching limits
  * **Programmatic Access using AWS Support API**

### Support Plans

#### Basic Support Plan

* **Customer Service & Communities** - 24x7 access to customer service, documentation, whitepapers, and support forums.
* **Trusted Advisor** - Access to the 7 core Trusted Advisor checks and guidance to provision your resources following best practices to increase performance and improve security.
* **AWS Personal Health Dashboard** - A personalized view of the health of AWS services, and alerts when your resources are impacted.

#### Developer Support Plan

* All Basic Support Plan Features
* **Business hours email access** to Cloud Support Associates
* Unlimited cases / 1 primary contact
* **Case severity / response times:**
  * General guidance: < 24 business hours
  * System impaired: < 12 business hours

#### AWS Business Support Plan (24/7)

* Intended to be used if you have **production workloads**
* **Trusted Advisor** – Full set of checks + API access
* 24x7 phone, email, and chat access to Cloud Support Engineers
* **Case severity / response times:**
  * General guidance: < 24 business hours
  * System impaired: < 12 business hours
  * **Production system impaired: < 4 hours**
  * **Production system down: < 1 hour**

#### Enterprise Support Plan (24/7)

* Intended to be used if you have mission critical workloads
* Access to a **Technical Account Manager (TAM)**
* **Concierge Support Team** (for billing and account best practices)
* **Infrastructure Event Management, Well-Architected & Operations Reviews**
* **Case severity / response times:**
  * General guidance: < 24 business hours
  * System impaired: < 12 business hours
  * Production system impaired: < 4 hours
  * Production system down: < 1 hour
  * **Business-critical system down: < 15 minutes**

## Advanced Identity

### Cognito

* Identity for your Web and Mobile applications users (potentially millions)

### Directory Services

#### AWS Managed Microsoft AD

* Create your own AD in AWS, manage users locally, supports MFA

#### AD Connector

* Directory Gateway (proxy) to redirect to on-premise AD

#### Simple AD

*  AD-compatible managed directory on AWS

### AWS Single Sign-On (SSO)

* Centrally manage Single Sign-On to access multiple accounts and 3rd - party business applications.
* Integrated with AWS Organizations

## Architecting & Ecosystem

### Cloud Best Practices – Design Principles

* **Scalability**: vertical & horizontal
* **Disposable Resources:** servers should be disposable & easily configured
* **Automation**: Serverless, Infrastructure as a Service, Auto Scaling…
* **Loose Coupling:**
  * Monolith are applications that do more and more over time, become bigger
  * Break it down into smaller, loosely coupled components
  * A change or a failure in one component should not cascade to other components
* **Services, not Servers:**
  * Don’t use just EC2
  * Use managed services, databases, serverless, etc

### Well Architected Framework 5 Pillars
#### Operational Excellence

* Design Principles
  * **Perform operations as code** - Infrastructure as code
  * **Annotate documentation** - Automate the creation of annotated documentation after every build
  * **Make frequent, small, reversible changes** - So that in case of any failure, you can reverse it
  * **Refine operations procedures frequently** - And ensure that team members are familiar with it
  * **Anticipate failure**
  * **Learn from all operational failures**

#### Security

* Design Principles
  * **Implement a strong identity foundation** - Centralize privilege management and reduce (or even eliminate) reliance on long-term credentials - Principle of least privilege - IAM
  * **Enable traceability** - Integrate logs and metrics with systems to automatically respond and take action
  * **Apply security at all layers** - Like edge network, VPC, subnet, load balancer, every instance,operating system, and application
  * **Automate security best practices**
  * **Protect data in transit and at rest** - Encryption, tokenization, and access control
  * **Keep people away from data** -  Reduce or eliminate the need for direct access or manual processing of data
  * **Prepare for security events** - Run incident response simulations and use tools with automation to increase your speed for detection, investigation, and recovery

#### Reliability

* Design Principles
  * **Test recovery procedures** - Use automation to simulate different failures or to recreate scenarios that led to failures before
  * **Automatically recover from failure** - Anticipate and remediate failures before they occur
  * **Scale horizontally to increase aggregate system availability** - Distribute requests across multiple, smaller resources to ensure that they don't share a common point of failure
  * **Stop guessing capacity** - Maintain the optimal level to satisfy demand without over or under provisioning - Use Auto Scaling
  * **Manage change in automation** - Use automation to make changes to infrastructure

#### Performance Efficiency

* Design Principles
  * **Democratize advanced technologies** - Advance technologies become services and hence you can focus more on product development
  * **Go global in minutes** - Easy deployment in multiple regions
  * **Use serverless architectures** - Avoid burden of managing servers
  * **Experiment more often** - Easy to carry out comparative testing
  * **Mechanical sympathy** - Be aware of all AWS services

#### Cost Optimization

* Design Principles
  * **Adopt a consumption mode** - Pay only for what you use
  * **Measure overall efficiency** - Use CloudWatch
  * **Stop spending money on data center operations** - AWS does the infrastructure part and enables customer to focus on organization projects
  * **Analyze and attribute expenditure** - Accurate identification of system usage and costs, helps measure return on investment (ROI) - Make sure to use tags
  * **Use managed and application level services to reduce cost of ownership** - As managed services operate at cloud scale, they can offer a lower cost per transaction or service

### Ecosystem

* **AWS Blogs**: https://aws.amazon.com/blogs/aws/
* **AWS Forums** (community): https://forums.aws.amazon.com/index.jspa
* **AWS Whitepapers & Guides**: https://aws.amazon.com/whitepapers
* **AWS Quick Starts**: https://aws.amazon.com/quickstart/
* **AWS Solutions**: https://aws.amazon.com/solutions/
* **Vetted Technology Solutions for the AWS Cloud**

* **Support:** 
  * Developer
  * Business
  * Enterprise
* **Marketplace**
  * Digital catalog with thousands of software listings from independent software vendors (3rd party)
  * You can sell your own solutions on the AWS Marketplace
* **Training**
  * AWS Digital (online) and Classroom Training (in-person or virtual)
  * AWS Private Training (for your organization)
* Professional Services & Partner Network
  * APN = AWS Partner Network
  * **APN Technology Partners:** providing hardware, connectivity, and software
  * **APN Consulting Partners:** professional services firm to help build on AWS
  * **APN Training Partners:** find who can help you learn AWS
  * **AWS Competency Program:** AWS Competencies are granted to APN Partners who have demonstrated technical proficiency and proven customer success in specialized solution areas.
  * **AWS Navigate Program:** help Partners become better Partners

