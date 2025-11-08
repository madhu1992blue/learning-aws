# AWS Global Infrastructure

## AWS Data Centers (DC)

- Physical facilities that contain the Infrastructure.
- For end users, there are no services to directly interact with the data centers of your choice.

## Availability Zones (AZ)

- Availability Zone is a collection of one or more Data Centers(DCs) that are co-located within a geographic area. (Usually walkable distance)
- They are connected to each other with low latency, high throughput(capacity), and redundant networking.
- A AZ is also an atomic unit of resource scope for non-global services.
- Each AZ also has a Physical ID associated with it. (e.g., usw2-az1, usw2-az2).
- However, users don't interact with Physical IDs directly. AWS maps Logical IDs to Physical IDs.
  - Users are expected to use Logical IDs and not Physical IDs (e.g., us-west-2a, us-west-2b) when deploying resources.

### NOTE:

- One cannot use Physical IDs of AZs
- There are account specific Logical IDs mapped to Physical IDs.
- The Logical IDs can vary between AWS accounts.
  - Hence, us-west-2a in one account may map to a different physical AZ than us-west-2a in another account.
  - This is done to ensure even distribution of resources across AZs as most people may tend to use AZs in alphabetical order.

## AWS Regions

- A Region is a collection of Physically AZs within a geographic area.
- In Each region, there are atleast 3 AZs. This is because some services like S3 require atleast 3 AZs for high availability.
- However, during initial rollout of a region, users may be able to access only 2 AZs. More AZs are added later.
- Data transfer between AZs within same region is guaranteed to be encrypted.
- Every Service in AWS has API endpoints terminated at Region level.
- Many services are deployed into large number of regions.
- Some services are only available in select regions.
- Resources provisioned in a service are scoped to a region. We cannot choose availability Zones or DataCenters.

## Local Zones

In some cases, where users might request Availability Zones in cities but AWS doesn't have a full region in that area, AWS deploys Local Zones which are associated or linked to a parent region.
These could be cities near a particular region but not in that region and users can opt-in to use these Local Zones for that particular region.
So, we can consider them Opt-in Extensions of a region.

## Edge Locations

These are separate from Regions. It's a parallel infrastructure that AWS maintains to deliver content closer to end users.
These could be Colocated space where AWS could be sharing space from another provider.
They have NW connectivity to region NWs.
They are not in AWS Data Centers.
Global Services are here. Ex: DNS, Content Caching.
There ~10x more Edge Locations than Regions.

## Scopes and Features

### Data Center Scope

Features that enable you to influence placement:
- Placement Groups:
  - Cluster: Pack instances closely together inside an AZ.
    Useful for HPC applications that need low latency and need node-to-node communication.
  - Partition: Spreads instances into logical partitions such that groups of instances in one partition do not share the underlying hardware with groups of instances in different partitions.
  - Spread: Spread instances across distinct underlying hardware to reduce correlated failures.
- Dedicated Instances: Run instances on hardware dedicated to a single customer.
- Dedicated Hosts: Physical servers dedicated for your use.

### Availability Zone Scope

### Offerings that fit in this scope

- EC2 Instances
- EBS Volumes
- RDS Databases
- FSx File Systems
- Redshift Nodes
- VPC subnet

### Multi-AZ Scope

Resources will still be present in one AZ but the services/features will enable you to choose more than one AZ at the same time.
Ex:
- RDS Multi-AZ deployment.
- Autoscaling on EC2
- Elastic Load Balancer
- Elastic Beanstalk environment

### Region Scope

- All Service API endpoints
- S3 Buckets
- DynamoDB Tables
- Lambda Functions
- WAF Web ACLs
- VPC - VPC service is region scoped but VPC subnets are AZ scoped

### Multi-Region Scope

- AWS Backup Plan
- S3 Replication
- RDS Read Replica
- Dynamo Global Tables


### Global Scopes

- Route 53 Zone
- CloudFront Distribution
- WAF Web ACL
- Lambda@Edge Function

### On-Premises Scope

- AWS Outposts
- AWS Snow-Family
- AWS Storage Gateway
- AWS IOT
