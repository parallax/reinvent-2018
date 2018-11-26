# Solutions Architect Associate Bootcamp

Everything based on Well Architected Framework.

AWS Certified Solutions Architect - Official Study Guide

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
