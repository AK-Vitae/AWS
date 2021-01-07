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



