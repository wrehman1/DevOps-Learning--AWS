# DevOps-Learning--AWS

## AWS Global Infrastructure

High availability - means that global infrastructure is able to diversify data centers to avoud downtime. 

## AWS Regions

AWS has has Regions all around the world. 

Names can be: us-east-1, eu-west-3 etc. 

Each region has multiple data centers, geographically isolated areas. 

Data centers are connected via high speed fibers. 

Factors to consider when choosing regions: ***Compliance***, ***Proximity*** (reduce latency?), ***Feature availability*** and ***Pricing***.


## AWS Availability Zones (AZs)

AZ is 1 or more data center within a region. 

Region is 3 or more AZ. 

Each region is completely isolated unless you explicitly allow data to be transferred to a different data center, good for security and or compliance. 

AWS has data centers across the world. they are separated from each other so that they are isolated from disasters. 

Regional services are by definition, already highly available. You don't want to run in one region because it needs to be fail proof. 

**BEST PRACTICE** - run across at least 2 AZs in one region. 

## Edge Locations (Points of Presence)

They are responsible for caching copies of data to be closer to the clients. This is done by **CONTENT DELIVERY NETWORK** (CDN). 

Amazon Cloudfront is a CDN. It helps deliver data, videos, API with low latency & high speed. 

**AWS Outposts** - make a mini region inside your own data center. 

**Amazon Route53** - is a Domain Name Service (DNS) that helps direct and route customers and translates domain names to IP addresses. 

## Identity & Access Management (IAM) 

`Users` - Mapped to a physical user, has password for AWS Console. 

`Groups` - Contains collection of related users only.

`Policies` - JSON document that outlines permissions for users and groups. Come in the form of allow/deny access to AWS services. 

`Roles` - Can be used by AWS services or for granting external access to accounts for EC2 instances or other AWS services. 

`Security` - MFA + password policy.

`AWS Command Line Interface (CLI)` - Manage AWS services using the Command Line.

`AWS Software Developer Kit (SDK)` - Manage AWS Services using a programming language. 

`Access Keys` - Access AWS using the CLI or SDK.

`Audit` - IAM Credential Reports & IAM Access Advisor. 

## Amazon EC2

EC2 = **Elastic Compute Cloud** = Infrastructure as a Service (IaaS)

EC2 is one of the most *popular* of AWS offering. 

It maining consists in the capability of: 

      • Renting virtual machinine (EC2).

      • Storing data on virtual drives (EBS).

      • Distributing load across machines (ELB).

      • Scaling the services using an auto-scaling group (ASG). 

## EC2 User Data

It is posibble to bootstrap our instances using an EC2 User Data script. Bootstrapping means launching commands when a machine starts. That script is *only run once* at the instance *first start*. EC2 User Data is used to automate boot tasks such as: 

• Installing updates

• Installing softwares

• Downloading common files from the internet

• Anything you can think of

The EC2 User Data Script runs with the root user. 

## EC2 Instance Types

<img width="795" height="717" alt="image" src="https://github.com/user-attachments/assets/437c185f-b3ea-40e1-b864-1f28978eb384" />

