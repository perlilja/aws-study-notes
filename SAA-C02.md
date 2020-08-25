# AWS Solution Architect Associate

## Tips and Tricks
### What is the exam focusing on
- 30% Design Resilient Architecture
- 28% Design Performant Architectures
- 24% Design Secure Applications and Architectures 
- 18% Design Cost-Optimized Architectures

### Other tips
- Understand differences between fault tolerant and high availability
- Assume that an answer using a single AZ is always incorrect.
- Managed services are preferred.
- For unstructured data S3 is a good solution.
- Look for caching options to improve performance.
- Know when to use auto scaling for a given architecture.
- Select the best instance size for a given workload.

### Exam Blueprint

#### Data Resilient Architectures
- Design a multi-tier acrhitecture solution.
- Design highly available and/or fault tolerant architectures.
- Design decoupling mechanisms using AWS services.
- Choose appropriate resilient storage.

#### Design High-Performing Architectures
- Identify elastic and scalable compute solutions for a workload.
- Select high-performing and scalable storage solutions for a workload.
- Select high-performing network solutions for a workload.
- Choose high-performing database solutions for a workload.

#### Design Secure Applications and Architecture
- Design secure access to AWS resources.
- Design secure application tiers.
- Select appropriate data security options.

#### Design Cost-Optimized Architectures
- Identify cost-effective storage solutions.
- Identify cost-effective compute and database services.
- Design cost-optimized network architectures.

### Whitepapers
- [Architecting for the Cloud: AWS Best Practices](https://s3.amazonaws.com/awsmedia/AWS_Cloud_Best_Practices.pdf)
- [AWS Security Best Practice](https://d1.awsstatic.com/whitepapers/Security/AWS_Security_Best_Practices.pdf)
- [Overview of Amazon Web Services](https://d0.awsstatic.com/whitepapers/aws-overview.pdf)
- [AWS Storage Services Overview](https://d0.awsstatic.com/whitepapers/AWS%20Storage%20Services%20Whitepaper-v9.pdf)
- [AWS Well Architected Framework](https://aws.amazon.com/architecture/well-architected/?wa-lens-whitepapers.sort-by=item.additionalFields.sortDate&wa-lens-whitepapers.sort-order=desc)
- [Overview of Security Processes](https://d1.awsstatic.com/whitepapers/aws-security-whitepaper.pdf)

### Videos
- [AWS Events Videos](https://www.youtube.com/channel/UCdoadna9HFHsxXWhafhNvKw)
- [Another Day, Another Billion Packets](https://youtu.be/3qln2u1Vr2E)

### Web pages
- [AWS Architecture Center](https://aws.amazon.com/architecture/)

### Key areas and services
- Application Integration
- Desktop & App Streaming
- Management Tools
- Analytics
- Migration
- Security, Identity & Compliance
- Compute
- Storage
- Databases
- Network & Content Delivery
- AWS Global Infrastructure

## Overview

- Availability Zone: Data Center (Could be one or many)
- Region: Geographical area, consist of 2 or more AZ.
- Edge location: Endpoints used for caching (CloudFront, CDN). There are more edge locations than regions (and AZ).

## Identity Access Management (IAM)
- Centralized control of your AWS account.
- Shared access to your AWS account.
- Granular permissions
- Identity federation (Google, LDAP, Facebook ...)
- Multifactor Authentication
- Temporary access for user/devices and services.
- Allows you to set up your own password rotation policy
- Integrates with many different AWS services.
- Supports PCI DSS Compliance

### Definition
- Users: End user
- Groups: A collection of users. Will inherit the group permissions.
- Policies: JSON documents, called policy documents. Give permissions as to what a user/group/role is able to do.
- Roles: You create roles and then assign them to AWS resources.

## AWS S3


## Design a Multi-tier Architecture Solution
- The VPC
- Subnets & Availability Zones
- Security Groups & NACLs
- Elastic Load Balancers
- AWS CloudFront

## Design Highly Available/Fault Tolerant Solutions
- Use Loose Coupling
- Avoid Tight Coupling
- Decoupling Using AWS Services
    - Decouple for Health using Queues.
    - Decouple for Scalability using Queues.
    - Decouple for Scalability using Elastic Load Balancer.
- Reliable/Resilient Storage
    - EC2 Instance Store
        - Ephemeral
        - Fixed capacity
        - Limited storage
    - Elastic Block Store
        - NAS
        - General Purpose SSD (gp2)
        - Provisioned IOPS SSD (io1)
        - Throughput Optimized HDD (st1)
        - Cold HDD (sc1)
    - Amazon EFS
    - Amazon S3
        - 11 9' durability
        - Encryption
    - Amazon Glacier
        - Design to be an archive solution
        
## Design High-Performing Architectures
    - Choose Performant Storage and Databases
        - EBS Volume Types
            - gp2 - SSD
            - io1 - SSD
            - st1 - HDD
            - sc1 - HDD
        - S3 Storage Classes
            - S3 Standard
            - S3 Infrequent Access (IA)
            - S3 Infrequent Access One Zone (IA-1AZ)
        - Databases
            - RDS (transactional queries)
            - Dynamo DB
            - Redshift (analytic queries)
        - CloudFront
            - Serve static and dynamic content
            - Protect private content (SSL and OAI)
            - WAF/Shield support
        - Elasticache (Memcached)
            - Caching databases
            - Horizontal scaling
            - Low maintenance
            - Storing session state
        - Elasticache (Redis)
            - NoSQL Databases (DynamoDB)
            - Vertical scaling
            - Atomic counters
            - Read replicas
            - Leaderboards/Counters
    - Design Solutions for Elasticity and Scalability
        - Horizontal (Instances/Services) vs. Vertical Scaling (CPU, RAMs)
        - Elastic Load Balancer
            - Launch Config (Instance size and IAM), can't be modified (only copied).
            - Auto Scaling Group, defines min and max.
            - Auto Scaling Policy, how much we should scale.
        - CloudWatch Metrics
            - Hypervisor level metrics (CPU utilization and network traffic)
            - Instance level matrics (disk space), needs a Cloudwatch Agent to be installed in the instance.
            - Default - 5 mins
            - Detailed - 1 min  
            - Cloudwatch Logs
            - Cloudwatch Alarms
    - Design for Scalability/Resilience
        - CloudFormation
           - JSON and YAML
           - Uses Stacks to create repetable and automatable configurations.
        - Autoscaling
        - Lambda
            - Fully managed compute service
            - Serverless
            
## Design Secure Applications and Architectures
    - Shared Responsibility Model
    - Principle of Least Privilege
    - Identity and Access Management (IAM)
        - Prefer assigning roles to resources over user accounts with access keys.
    - VPC
    - Security Groups and NACLs
        - Only NACLs have DENY rules
        - Security Groups applied at Elastic Network Interface (ENI)
        - NACLs applied at Subnet level
    - Subnets
        - Public vs Private
        - Public must contain a Internet Gateway, Route Table entry to Internet Gateway and a Public IP Address.
        - Private subnets needs access to a NAT Gateway or a NAT instance to access the internet.
    - Securing the Data
        - Data in transit
            - SSL, IPSec VPN, Direct Connect with IPSec
        - Data at rest
            - SEE-S3, SSE-KMS, SSE-C, Client side encryption
    - Key Storage and Management
        - AWS KMS
    
            
          

    
    
      
            
            
        
        


