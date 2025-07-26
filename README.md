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

## Vertical Scalability

Vertical scalability means ioncreasing the size of the Instance. For example, your application is running on a t2.micro, scaling it veritically would mean to upgrading the instance to a t2.large, same server but more ~RAM, CPU and storage. 

Veritcal scalability is very common for non-distributed systems, such as databases.

RDS, ElastiCache are services that can scale vertically. T
There usually is a limit to how much you can vertically scale (hardware limit).

## Horizontal Scalability

Horizontal Scalability means increasing the number of instances/systems for your application. 

Hotizontal scaling implies distributing systems. This is very common for aweb applications/modern applications.

It's easy to horizontally scale thanks to the Clolud offerings such as Amazon EC2. 

Horizonrtal scalibility is also known as elastic. If one instance fails. there will be other instances available to handle and continue as a server. 

## High Availability 

• High availability usially goes hand in hand with horizontal scaling.

• HA means running your application/system in at least 2 data centers (== Availability Zones).

• The goal of HA is to survive a data center loss. 

• The HA can be passive (for RDS Multi AZ for example). 

• The HA can be active (for Horizontal Scaling). 

## HA & Scalability for EC2 

• Vertical Scaling: Increase instance size (scale up/down) from t2.nano to u-12tb1.metal

• Horizontal Scaling: Increase number of instances (scale out/in)

      Use: Auto Scaling Group and Load Balancerto help with scaling.

• High Availability: Run instances for the same applications across multi-AZ 

      Use: Auto Scaling Group multi-AZ nad load Balancer multi-AZ to make sure app is running smootly. 

## Load Balancer (LB)

Loand balancers are servers that forward traffic to multiple servers (e.g. EC2 instances) downstream. 

In AWS, ELB sits between users and EC2 instances. When traffic comes in, it forwards the traffic to EC2 downstream. It is constantly checking which instances are healthy and direct the traffic to the ones that can handle it. 
This process keepsthe application available and responsive, even if one more instances fail. 

Revers eproxies are same as LB but with extra functionality. It also sits between users and servers handling requests but it can do more than just traffic 

Load balancers constantly check the health of EC2 instances. Load balancers not just handle traffic, but manage failover, security and ensures high availability across multiple AZs. 

## Why use Elastic Load Balancer (ELB)?

An Elastic Load Balancer is a mangaed load balancer:

      • AWS guarantees that it will be working.

      • AWS takes care of upgrades, maintenance, high availability.

      • AWS provides only a few configuration knobs.

It costs less to setup your own load balancer but it will be a lot more effore on your end. 

ELB is integrated with many AWS offerings/services:

      • EC2, Ec2 Auto Scaling Groups, Amazon ECS

      • AWS Certificate Manager (ACM), CloudWatch

      • Route53, AWS WAF, AWS Global Accelerator

## Health Checks

Health Checks are crucial for Load Balancers.

They enable the load balancer to know if instances it forwards the traffic to are available to reply to requests. 

Health Cheks are done on a port and a route (/health is common)

If the response is not 200 (OK), then the instance is unhealthy. 

## Application Load Balancer (ALB)

• Application Load Balancers is Layer 7 (HTTP).

• It has the ability to load balanced traffic to multiple HTTP applications running across different machines all within  target groups, e.g EC2 instances, Lambda functions and even containers.

• Load balancing to multiple applications on the same machine ex containers. 

• Support for HTTP/2 and WebSocket.

• Supports redirects (e.g. from HTTP to HTTPS) - better performance and more connections. 

• Routing tables to different target groups.

• Routing based on path in URL and hostname in URL. 

• ALB are a great fit for micro services & container-based application (E>G> Docker & Amazon ECS).

• Has a port mapping feature to redirect to a dynamic port in ECS. 

• ALBs uses health checks to ensure the instances in each group are running and able to handle traffic. If health check fails - meaning an instance is not responding or is in trouble, the ALB will stop sending traffic to that instance and instead route request to other instances in the group.

• ALB is built for HTTP and HTTPS traffic, meaning it can handle a wide range of web-based services.

• ALB will examine each request and looks at where to send the traffic based on the path host or other writing that have setup. 

• A search request would be requested to a separate target group focused on search related functionality 

• by using different and target groups, you can ensure that one service doesn't interfere with the other, allowing your application to scale and perform better. 

## Network Load Balancer (NLB)

These are optimised for handling extreme performance and high traffic with low latency. 

Network load balancers (operate at Layer 4 - Transport Layer of OSI model) and allow to: 

      • Forward TCP and UDP traffic to your instances 

      • Handle millions of request per seconds

      • Less latency ~ 100ms (vs 400ms for ALB)

NLB has one static IP per AZ and supports assigining Elastic IP (helpful for whitelisting specific IP)

NLB are used for extreme performance, TCP or UDP traffic. 

Not included in the AWS free tier. 

NLB focuses on speed and efficiency at layer 4 - making it perfect for handling millions of requests with minimal latency. By fowarding TCP directly, it lets you handle large amounts of data quickly which make it ideal for applications with high demands for performanc and scalability. 

## Sticky Sessions (Session Affinity)

• Sticky sessions ensure that the client is always routed to the same instance behind a load balancer. 

• This works for Classic Load Balancer, Application Load Balancer and Network Load Balancer. 

• For CLB and ALB, the "cookie" used for stickiness has an expiration date you control. 

• Sticky sessions should be used when an application stores session data 

• Enabling Stickiness may bring imbalance to the load over the banckend EC2 instances. 

• Only use sticky sessions when user session data isn't shared across multiple instances. 

• If your handling critical session data that needs to stay with one server, it is good to use sticky sessions. Hoever, if load balance and efficiency is more important & you haven't got data to maintain in one place, it may best to think about before enabling it. 

## SSL/TLS Basics 

These are crucial when dealing with security in the onternet, especially for load balancers that handle traffic between clients and server. 

• An SSL Certificate allows traffic between your client's and your load balancer to be encrypted in transit (often called in-flight encryption). This means that data is scrambled as it travels over the internet, preventing from anyone snooping on it.  

      • SSL refers to Secure Sockets Layer, used to encrypt connections. 

      • TLS refers to Transport Layer Security, which is a newer version. This is the modern version of SSL.

• Nowadays, TLS certificates are mainly used, but people still refer as SSL. 

• Public SSL certificates are issued by Certificate Authorities (CA). Examples are: Comodo, Symantec, GoDaddy, GlobalSign, Digicert, Letsencrypt (more popular) etc. 

• SSL certificates have an expiration date (set by yourself) and must be renewed after 1, 2 or even 10 years. 

## Load Balancers - SSL Certificates 

• The load balancer uses an X.509 certificate (SSL/TLS server certificate)

• Certificates are managed by using AWS Certificate Manager (ACM) or certificates can be uploaded manually. 

HTTPS listener: 

      • Specify a default certicate 

      • List of certs to support multiple domains can be added optionally. 

      • Clients can use Server Nane Indication (SNI) to specify the hostname they reach

      • Ability to specify a security policy to support older versions of SSL/TLS (legacy clients).

## SSL - Server Name Indiciation (SNI)

• SNI solves the problem of loading multiple SSL certificates ontpo web servers (to serve multiple websites).

• Newer protocol so requires the client to indicate the hostname of the target server in the initial SSL handshake. 

• Server will find the correct certificate or it will return thew default one. 

NOTE: Only works for ALB & NLB (new gen) / CloudFront. 

## Elastic Load Balancer - SSL

Classic Load Balancer (v1):

      • Supports only one SSL cert.

      • Must use CLB for multiple hostname with multiple SSL certs. 

Application Load Balancer (v2):

      • Supports multiple listener with multiple SSL certs

      • Uses server name indication (SNI) to make it work

Network Load Balancer (v2):

      • Supports multiple listener with multiple SSL certs

      •  Uses server name indication (SNI) to make it work

## Connection Draining 

On AWS, this is known as Deregistration Delay. 

• Feature Naming: 

      - Connection Sraining - for CLB

      - Deregistration Delay - for ALB & NLB

• Time to complete in-flight requests while the instance is re-registered or unhealthy. 

• Stops sending new requests to the EC2 instance which is de-registering.

• Between 1 to 3600 secs (default: 300 secs)

• Can be disabled (set value to 0)

• Set a low value if reqs are short. 

## Auto Scaling Groups (ASG)

Load on websites and apps can changes drastically. In the Cloud, servers can be created and removed very fast. 

The goal of ASG is to: 

      • Scale out (add EC2 instances) to match an increased load. 

      • Scale in (remove EC2 instances) to match a decreased load. 

      • Ensure  a min amd max number of EC2 instances running. 

      • Auto register new instances to a load balancer. 

      • Recreate an EC2 instance in case old is terminated or is unhealthy.

      • ASG is free, only pay for EC2 they manage. 


















      
