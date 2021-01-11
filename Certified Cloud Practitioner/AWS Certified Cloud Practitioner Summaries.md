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

