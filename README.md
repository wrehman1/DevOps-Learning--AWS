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

## Auto Scaling Groups in AWS

ASG operates based on 3 things: Minimum capacity, Desired capacity and Maximum capacity. 

Minumum capacity - the least number of EC2 instances that are running, even during low traffic times. 

Desired capacity - target number of instances for normal load. ASG will try and maintain this number unless something changes.

Maximum capacity - Most number of EC2 instances that the ASG is allowed to scale up during high traffic periods. 

## ASG in AWS with Load Balancer

<img width="656" height="334" alt="image" src="https://github.com/user-attachments/assets/8b3f2bfe-52cc-4ff4-a2d1-72fa7b9fca82" />

• The ALB works as the distributor of the incoming traffic to the EC2 instances. It spreads the load so no EC2 instance gets overwhelmed. The ALB checks the health of the EC2 instances, if one does go down, it stops sending traffic to it. 

• The regional health checks - Check for unhealthy or faulty EC2 instances and route traffic from the faulty one until its back online or replaced by the ASG. 

• ASG automatically adjusts the number of the EC2 instances to match the current load. E.g when a website experiences heavy traffic on a sales day, the ASG will scale out. When traffic decreases, the ASG will scale in to reduce the number of instances to save costs. 

## Auto Scaling - CloudWatch Alarms & Scaling

• It is possible to scale an ASG based on CloudWAtch alarms.

• An alarm monitors a metric (such as Average CPU, or a custom metric).

• Metrics like Average CPU are computed for the overall ASG instances. 

• Based on the alarm: 

      - We can create scale OUT policies (increase number of instances)

      - We can create scale IN policies (decrease number of instances)

## ASG - Scaling Policies 

<img width="536" height="239" alt="image" src="https://github.com/user-attachments/assets/3a97022e-28b1-43a6-98d8-667e818f28be" />

## Container related Services on AWS 

• Elastic Container Service (ECS): Is an AWS managed container service. 

• Elastic Kubernetes Services (EKS): Is an AWS managed Kubernetes service.

• AWS Fargate: Serverless containers abstracting away infrastructure manaagement. 

• Amazon Elastic Container Repository (ECR): Is an AWS Docker image storage & management service, AWs version of DockerHub. 

## Amazon ECS 


EC2 Launch Type:

<img width="626" height="331" alt="image" src="https://github.com/user-attachments/assets/0c47ae9c-3f9d-43e0-8089-e65f0395c523" />


Fargate Launch Type: 


<img width="646" height="247" alt="image" src="https://github.com/user-attachments/assets/fb330458-e37f-4c0c-9d97-8233b08e3412" />


IAM Roles for ECS: 


<img width="673" height="314" alt="image" src="https://github.com/user-attachments/assets/1843890a-a1ee-4232-a160-6e24b883dc5e" />



Load Balancer Integrations:


<img width="660" height="316" alt="image" src="https://github.com/user-attachments/assets/9b8c8976-1199-4ec3-98a8-4eb02b224c7c" />


## ECS Service Auto SCaling 

• Automatgically increase/decrease number of ECs tasks.

• Amazon ECS Auto Scaling uses AWS Application Auto Scaling. 

• **Target Tracking** - Scale based on target value for a specific CloudWatch metric

• **Step Scaling** - Scale based on specified CloudWatch Alarm. 

• **Scheduling Scaling** - Scale based on a specified date/time (predictable changes).

• ECS Service Auto Scaling (task level) = EC2 Auto Scaling (EC2 instance level)

• Fargate Auto Scaling is much easier to setup (because it is Serverless)

ECS Auto scaling ensures that services can handle spikes without any problems and spikes down when traffic is low.  

## Amazon ECR - Elastic Container Registry

• ECR stores and manages Docker images on AWS. 

• Private and Public repo (Amazon ECR Public Gallery)

• Fully integrated with ECS, backed by Amazon S3. 

• Access is controlled through IAM permissions ( any errors - check permissions).

• Supports image vulnerability s canning, versioning image tags, image lifestyles. 

## Amazon EKS - Elastic Kubernetes Service

• Enables user to launch *managed Kubernetes clusters* on AWS 

• Kubernetes - an *open-source system* for automatic deployment, scaling and management of containerised (usually Docker) app. 

• Its an alternative to ECS - similar goal but different API.

• EKS supports EC2 if worker nodes need to be deployed or Fargate to deploy serverless containers. 

• Case study: If a company is already using Kubernetes on-prem or in another cloud and wishes to migrate to AWS using Kubernetes. 

• **Kubernetes is cloud-agnostic** (can be used in any cloud - Azure, GCP etc). 

• For multiple regions, deploy one EKS cluster per region. 

•Collect logs and metrics using **CloudWatch Container Insights**

<img width="728" height="355" alt="image" src="https://github.com/user-attachments/assets/ddf08fc3-ce27-43d4-9ed5-8a2cd8ff0b0a" />

• EKS nodes - These are EC2 instances where containers and pods actually run. 

• ELB - Directs user traffic to the nodes and distributes evenyly. 

• Nat Gateway (NGW) - Allow nodes to pull updates/images from internet without exposing them directly to the public traffic. 

• Private Subnets - Keep everything secure and isolated and are spread across multiple AZs, ensuring app is always available.

## Amazon EKS - Node Types 

• Managed Node Groups

      - AWS creates and manages nodes (EC2 instances) for you.

      - Nodes are part of an ASG Managed by EKS - automatically adjust the amount of nodes needed. 

      - Supports On-Demand or Spot Instances

• Self-Managed Nodes

      - Nodes created by user and registered to the EKS cluster and managed by an ASG.

      - You can prebuilt AMI - Aamzon EKS optimised AMI (Amazon Machine Image). 

      - Supports On-Demand or Spot Instances 

• AWS Fargate 

      - No maintenance needed - no nodes managed.

      - Just define CPU and memory requirments for containers, AWS Fargate takes care of everything

      - Easy to manage, but can be expensive 



## Serverless 

<img width="592" height="240" alt="image" src="https://github.com/user-attachments/assets/25abd8c9-377f-41d5-8c2e-76eaf14d7e6c" />

## Serverless in AWS 

<img width="561" height="330" alt="image" src="https://github.com/user-attachments/assets/94510ff6-4350-4aa6-803c-4b4f582c5b4f" />

## EC2 vs Lambda

<img width="551" height="244" alt="image" src="https://github.com/user-attachments/assets/feb91605-f51c-46cd-ae1a-b412767312ee" />

## AWS Lambda Language Support

<img width="551" height="253" alt="image" src="https://github.com/user-attachments/assets/d4468b5d-204c-421e-aea0-8e9c573f7519" />


## AWS Networking 

CIDR (IPv4) - Classless Inter-Domain Routing:

• Way of allotcating IP addresses. 

• Help define IP ranges. 

## Subnet Masks 

<img width="701" height="298" alt="image" src="https://github.com/user-attachments/assets/8b32d0ca-4dbf-477b-b0ff-aeb109254015" />

## Subnet (IPv4)

<img width="815" height="388" alt="image" src="https://github.com/user-attachments/assets/4629b460-da54-40f8-98fa-bfcdf961b6e4" />

## Internet Gateway (IGW)

<img width="561" height="248" alt="image" src="https://github.com/user-attachments/assets/2f192eec-d3c7-43fd-8a21-acddbe0915ba" />

## Bastion Hosts

<img width="840" height="424" alt="image" src="https://github.com/user-attachments/assets/5ce1c569-c8d6-41cc-a3b7-498128615af2" />


## NAT Gateway

NAT Gateway is a powerful tool for allowing private subnets to reach the internet without exposing directly. 

<img width="823" height="278" alt="image" src="https://github.com/user-attachments/assets/42ca69e9-706d-44ef-9f5c-95d1d47280d6" />

<img width="861" height="469" alt="image" src="https://github.com/user-attachments/assets/9f4a201f-a71d-48b5-a52f-e94e5e782b04" />

## NAT Gateway VS NAT Instance 

<img width="851" height="358" alt="image" src="https://github.com/user-attachments/assets/bd6e6aa4-f845-457c-acd1-ef77fb102501" />

## Network Access Control List (NACL)

<img width="827" height="389" alt="image" src="https://github.com/user-attachments/assets/15fbbff1-f68d-4517-8ab3-f3b8a3b568e5" />

      
## VPC Summary 

<img width="600" height="273" alt="image" src="https://github.com/user-attachments/assets/ec7ae8b0-2414-47cf-ac59-871f55557d3a" />

<img width="593" height="273" alt="image" src="https://github.com/user-attachments/assets/33aa00fe-5e82-4e74-a07a-106afd8ceb76" />


## AWS Assignment Part 1

Objective: 

Create a custom VPC with both public and private subnets, configure internet access, and deploy EC2 instances with secure segmentation.

<img width="678" height="533" alt="image" src="https://github.com/user-attachments/assets/6fb5afd5-0c31-4ee8-b0f8-011cc1f380bb" />

<img width="1408" height="261" alt="image" src="https://github.com/user-attachments/assets/58ed4e53-1ca6-4750-8231-ae0a7ec7a5b0" />

## AWS Assignment Part 2 - Application Load Balancer

Objective: 

Deploy an Application Load Balancer (ALB) with two EC2 instances behind it. Ensure security group (SG) configurations allow only ALB access to EC2 instances while preventing direct access. 


<img width="649" height="95" alt="image" src="https://github.com/user-attachments/assets/5009404c-5a33-49cc-932f-cca6437c56dc" />

<img width="915" height="190" alt="image" src="https://github.com/user-attachments/assets/b2668c7f-335b-4de4-8bad-e32415e5b696" />

<img width="907" height="197" alt="image" src="https://github.com/user-attachments/assets/733fa1b8-4052-4faf-b0ff-3b609b41f5b8" />

<img width="1453" height="321" alt="image" src="https://github.com/user-attachments/assets/1e940814-790b-4460-b2b7-21f93a1b148e" />

<img width="674" height="511" alt="image" src="https://github.com/user-attachments/assets/33c56bc9-da3d-4769-892c-0d46854cc943" />

<img width="906" height="187" alt="image" src="https://github.com/user-attachments/assets/e1dd6663-1f1e-47bf-8923-bc5bfcaee98e" />

<img width="907" height="174" alt="image" src="https://github.com/user-attachments/assets/52caa6e7-f3bc-4823-b63b-fd54e45cdfd7" />

<img width="745" height="239" alt="image" src="https://github.com/user-attachments/assets/ffb6c6d9-dba3-4bea-a77e-a2de5cac22f3" />





















