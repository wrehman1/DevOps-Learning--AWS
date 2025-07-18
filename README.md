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

## EC2 Instances Purchasing Options

<img width="808" height="396" alt="image" src="https://github.com/user-attachments/assets/52a0b957-025c-42ae-8651-a331ac42cfaa" />

## Security Groups

Secority Groups are the fundemental of network security in AWS. They control how traffic is allowed in or out of your EC2 Instances. SG's only allow rules. SG rules can reference by IP or by SG.

SGs are acting as a "Firewall" on an EC2 Instance. They regulate: 

      • Access to Ports

      • Authorised IP ranges - IPv4 and IPv6

      • Control of inbound network (from other to the Instance)

      • Control of outbound network (from the Instance to the other)


• SG can be attached to multiple Instances. 

• SG can be locked down to a region/VPC combination.

• SG does live "outside" the EC2 - if traffic is blocked, the EC2 Instance won't see it. 

• It is good practice to maintain one separate SG for SSH access. 

• If your application is not accessible (times out), then it's a SG issue. 

• If your application gives a "connection refused" error, then it's an application error or it's not launched.

• All inbound traffic is blocked by default.

• All outbound traffic is authorised by default.


## Ports

`22 = SSH (Secure Shell)` - log into a Linux Instance

`21 = FTP (File TRanfer Protocol)` - Upload files into a file share

`22 = SFTP (Secure File Transfer Protocol)` - Upload files using SSH

`80 = HTTP` - Access unsecured websites

`443 = HTTPS` - Access secured websites

`53 = DNS` - For DNS queries and resolving

`3389 = RDP (Remote Desktop Protocol)` - Log into a Windows Instance

## Private vs Public (IPv4) Differences

<img width="441" height="518" alt="image" src="https://github.com/user-attachments/assets/dcdf7370-8567-46b6-8f20-6737b2a162b6" />

## Elastic IPs

When you stop an then start an EC2 Instance, it can change its Public IP.
If you need to have a fixed Public IP for the Instance, you will need an Elastic IP. 
An Elastic IP is a public IPv4 IP which you own as long as the Instance is not stopped or terminated. 
An Elastic IP can only be attached to one Instance at a time. 

## Elastic Block Store (EBS) Volume

An Elastic Block Store (EBS) volume is a network drive you can attach to your instances while they run. 
It Allows your instances to persist data, even after termination. 
They are bound to a specific availability zone. 
They act as a network USB stick. 
Solid State by default. 

## Amazon Machine Image (AMI)

AMI are a customisation of an EC2 Instance: 
      • You add your own software, configuration, operating system, monitoring

      • Faster boot / configuration time because all your software is pre-packaged

AMI are built for a specific region (and can be copied across regions)

EC2 Instances can be launched from: 

      • A Public AMI: AWS provided

      • Your own AMI: You can make and maintain them. 

      • An AWS Marketplace AMI: an AMI created by someone else and want to sell it to other users. 

## Amazon Elastic File System (EFS)

Amazon EFS is a managed Network File System (NFS) that can be mounted on multiple EC2 Instances at the same time, great for use cases which a large number of servies & resources need access to the same data.

Managed file system - traditionally store on--premises. 

EFS can work with many EC2 Instances across multi AZs. 

EFS is scalable, highly availbale but can be very expensive - it is best to use it when an application truely needs shared storage across multiple instances 




















































      
