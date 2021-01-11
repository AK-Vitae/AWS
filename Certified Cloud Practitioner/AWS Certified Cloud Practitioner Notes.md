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
* Managed NFS (network file system) that can be mounted on 100s of EC2
* EFS works with Linux EC2 instances in multi-AZ
* Highly available, scalable, expensive (3x gp2), pay per use, no capacity planning

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