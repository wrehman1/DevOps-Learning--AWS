# DevOps-Learning--AWS

## AWS Global Infrastructure

High availability - means that global infrastructure is able to diversify data centers to avoud downtime. 

## AWS Regions

AWS has fault tolerance and has regions. 

Each region is completely isolated unless you explicitly allow data to be transferred to a different data center, good for security and or compliance. 

Each region has multiple data centers, geographically isolated areas. 

Data centers are connected via high speed fibers. 

Factors to consider when choosing regions: ***Compliance***, ***Proximity*** (reduce latency?), ***Feature availability*** and ***Pricing***.

## Edge Locations 

They are responsible for caching copies of darta to be closer to the clients. This is done by **CONTENT DELIVERY NETWORK** (CDN). 

Amazon Cloudfront is a CDN. It helps deliver data, videos, API with low latency & high speed. 

**AWS Outposts** - make a mini region inside your own data center. 

**Amazon Route53** - is a Domain Name Service (DNS) that helps direct and route customers and translates domain names to IP addresses. 

## Availability Zones (AZs)

AZ is 1 or more data center within a region. 

Region is 3 or more AZ. 

AWS has data centers across the world. 

Regional services are by definition, already highly available. You don't want to run in one region because it needs to be fail proof. 

**BEST PRACTICE** - run across at least 2 AZs in one region. 
