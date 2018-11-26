# Solutions Architect Associate Bootcamp

Everything based on Well Architected Framework.

[ ] Buy the AWS Certified Solutions Architect - Official Study Guide

Domains:
- Design Resilient Architectures
- Define Performant Solutions
- Specify Secure Applications and Architectures
- Design Cost-optimised Architectures
- Define Operationally Excellent Architectures

130 minutes for the exam
65 questions

Don't second guess yourself, think questions through the first time.

No penalty for guessing.

1. Read question and answer in full
2. Identify the features mentioned in answers.
3. Identify text in question that implies certain features
4. Pay attention to qualifying clauses
5. Eliminate obviously wrong answers

http://reinvent2018.vstbridge.com/

Set up account

Amazon EC2 Instance Store
- Ephemeral volumes
- It's a boot disk
- Only certainly EC2 instances
- Fast access to disk
- Disk type and capacity depends on instance type
- Not worried about persistence

EBS
- This has persistence
- Provides block level storage
- Attached in same AZ as EC2
- Persists independent of instances

EBS Volume Types table - memorise IOPS.

Where to fill your gaps:
All FAQs on certification on exam prep page

A, C, D plausible

IOPS read/write issue

## Load balancers

Classic load balancer 4 and 7

Network Load Balancer - TCP
Application Load Balancer - HTTPS

[ ] Read FAQs for SQS, ELB, EC2
[ ] Route53 Documentation

SQS, ELB

## EFS

Mount across multiple AZs, petabyte scale, NFS.

aws.com/architecture - Quick Starts and Reference Architectures

Spend a lot of time studying those.
[ ] Absolutely crucial that you know where things sit, in AZ/subnet etc

## S3

- No charge for upload
- Each object 5TB, encrypt at rest/transit
- Lifecycle management

[ ] Be familiar with encryption Types

Object ACLs
Bucket ACLs
Bucket policies
IAM policies

Where would you use each one of these.

## Glacier

Vaults/archives - use for backup and archiving - takes longer to get it out.

Focus on S3 and glacier
Be familiar with EFS and CloudFront

Use free-tier and play around

## EC2

Remember screens of building an EC2 in the console. Pick instance size,
how many, placement group, assign IAM, VPC / AZ, know the options on the 3rd screen
it'll really help you. Next screen storage.

Tightly coupled - web server / app server - will fail.

[ ] Read the AWS Well Architected Framework - at least the top-level

## CloudFormation

[ ] You should be able to read a definition and know roughly what it does.

Template creates a 'stack' of resources in a reproducible manner.

AMI IDs are different in each region.

Params are for users to enter inputs.

## Exam consideration

It's 6 months before a feature makes it way into an exam.

- Lambda - timeouts are 5 mins
- Single AZ will never be right answer, always 2. More for spot.
- Using AWS managed
- Using AWS managed services is always preferred
- Fault tolerant and highly availability are different
  - Fault tolerance is recovering automatically
  - High availability is can we get to the instance if one fails
- Expect that everything will fail at some point and design accordingly

## Domain 2 - Designing Performant Architectures

2.1 Choose Performance Storage and DBs

[ ] Know the 4 types of EBS
[ ] Know the IOPS

## S3 buckets

[ ] Know the storage classes
[ ] Know the pricing models

Know about VPC endpoints, can connect directly to an S3 buckets

S3 objects are immutable
Unlimited objects

## Databases

[ ] Know at least RDS, DynamoDB, Redshift at a high level

## RDS

- Read replicas live inside an AZ.
- Standby can live in another AZ

### DynamoDB

Provisioned throughput

- Fixed allocation, not the new dynamic scaling -- that won't be in the exam

Read capacity units 4KB
- One for strongly consistent read per second
- Two eventually consistent reads per second
Write capacity units 1KB
- One write per second

Need to be able to calculate this on the exam.

##  Caching

### CloudFront

Caching with CloudFront, HTTP requests.

(Skipped a fair few notes as I'm quite familiar here)

### ElastiCache

ElastiCache can be put in front of DynamoDB, RDS.

memcached and redis flavours.

[ ] Know the differences between

Redis is much more complex.

memcached

- Multithreading
- Low maintenance
- Easy horizontal scalability with Auto Discovery

Redis

- Support for data structures
- persistence
- Atomic operations
- Pub/sub messaging
- Read replicas/failover
- Cluster mode/sharded clusters

### Designing solutions for scaling

Vertical: (scale up/down)
Small instance -> large

Horizontal: (scale in/out)
Change number of instances

EC2 Auto scaling
- Launches or terminates instances
- Automatically register new instances with load balancers
- Can launch across multiple AZ
- Integrates with ELB

AWS Auto scaling
- Manage scaling for multiple resources across multiple services
- Predefined scaling strategies available

Amazon EC2 Auto scaling
- Only need to manage and scale EC2 Auto Scaling groups
- Only interested in maintaining the health of your EC2 fleet

You need to monitor in a solution such as CloudWatch.

Can monitor:

- CPU
- Network
- Queue size
- Custom metrics

ELB

Key point: you can not load balance across regions.

Route53 would be used to balance across regions.

Implementing Continuity:

```
Resources -> CloudWatch -> CloudWatch alarms
      ^                            v
      `------------     Auto Scaling Policy
```

- Memory is not a native CloudWatch event

Exam considerations

- If caching is on the answer, it's probably that (to improve performance)
- If data is unstructured, it's S3
- Know when and why to use Auto scaling
- Choose the instance and database type that makes the most sense for your workload

# Domain 3 - Specify Secure Applications and Architectures

3.1 Determine how to secure application tiers
3.2 Determine how to secure data
3.3 Define the networking infrastructure

The shared responsibility model is the most important slide in any course.

Fundamental that everything is understood.

Customers secure: You secure IN the cloud
- Customer Data
- Platforms, apps, Identity & Access management
- Operating System, Network & Firewall Configuration
- Client-Side Data encryption
- Server-Side Data encryption
- Network Traffic Protection

Amazon secures: They're responsible for the security OF the cloud
- Foundation services
  - Compute
  - storage
  - Database
  - Networking
Infrastructure:
- Availability Zones
- Regions
- Edge locations

## AWS IAM

- Centrally manage users and user permissions
- Control which AWS resources users/applications can access
- Create users, groups, roles and policies
- Integrates with Microsoft Active Directory and AWS Directory Service
- Principle of Least Privilege

Identities:
- IAM Users and groups
- IAM Roles
- Federated Users (AD etc)
- Web Identify Federation (Cognito)

Look at "When to Use AWS STS"

IP restrictions are a whack-a-mole and not currently supported.

Roles are temporary credentials

## Data In-transit

- SSL/TLS
- VPN
- Import export/snowball
- Direct connect is in the exam

Data sent to the AWS API

- AWS API calls use HTTPS
- All signed with Sigv4

CloudTrail -- traces

## Data at rest in S3

Priva

te by default

Access of HTTP or HTTPS
Audit of access to all objects
Supports resource-based policies
- buckets
- Prefixes
- objects

Server-side encyptions

- S3 managed
- KMS-Managed
- Customer provided keys

Client-Side encryption

- KMS-Managed Customer Master Key (CSE-KMS)
- Client-side Master Key (CSE-C)

KMS is a management services that rotates keys automatically.

DynamoDB supports encryption at the row-level

SES potentially mentioned in the test.

EBS - Encrypted at the volume level

CloudHSM is hardware-based key management

Keys are managed only by the customer

FIPS 140 Level 3  is CloudHSM

Pricing for KMS is per dollar per call

[ ] Watch the Protecting Your Data in AWS video
[ ] Read the Encrypting Data at rest whitepaper

S3 is a major topic in this exam.

A
