

# AWS SSA Exam - Outstanding Knowledge


## Ephemeral Disks / Instance Stores
*Question: Does an Instance Store persist between a restart cycle? a start/stop cycle? a termination?*

An Instance Store Volume provides temporary (ephemeral) block level storage. This storage is physically attached to the host compute on which a (virtualized) EC2 Instance runs. The maximum size for a root device backed by an Instance Store Volume is 10GiB.

Instance Stores Volumes can only be specified at launch-time of an EC2 Instance. An Instance Store Volume can't be detached from one Instance and re-attached to another.

An Instance Store Volume must be mounted and formatted before it can be used.

The data help on an Instance Store Volume persists only for the life-time of the instance. It persists between an instance reboot, however it is lost under the following conditions:

- The underlying (physically attached) disk fails
- The Instance is stopped (in fact, the Instance Store Volume will not be present when the Instance is subsequently started)
- The Instance is terminated

Instance Stores Volumes are included in the hourly cost of the Instance.

## Placement Groups
*Question: What are they, how are they used, are they cross-A-Z, cross-Region etc.*

A _Placement Group_ is a logical grouping of EC2 Instances within a single Availability-Zone. They are recommended for instances that benefit high network throughput, low network latency, or both. The instance type MUST support __Enhanced Networking__.

A Placement Group is created and then instances are launched into it. AWS recommend that instances are launched together in a single launch request and that the same Instance Type is used. An 'Insufficient Capacity Error' may be thrown if an instance is subsequently launched or if a different Instance Type is launched at a later date/time.

Placement Groups can't span multiple Availability-Zones.

There is no charge for creating a Placement Group.

## Trusted Advisor
*Question: What is it, what does it report on, what areas does it cover?*

https://aws.amazon.com/premiumsupport/trustedadvisor/

Inspects an AWS environment and makes recommendations based on the following areas:

CPS+FT = 
- C - Cost Optimization
- P - Performance
- S - Security
- FT - Fault-Tolerance

Available to all customers - Security and Performance (core checks)
Available to customers with Business or Enterprise support plans (all checks)

## CloudWatch
*Question: What is the minimum interval for CloudWatch metrics?*

## Consolidated Billing
*Question: What are the two different types of account?*

## EBS & Instance Store Volumes
*Question: What are the Key differences between EBS and instance-store backed volumes*
http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ComponentsAMIs.html

- EBS Volumes perserve their data between instance stops and terminations (with the necessary flags set); Instance Store Volumes do not.
- EBS Volumes can be easily backed-up with EBS snapshots to durable S3 storage; data on Instance Store Volumes must employ a custom backup strategy.
- EBS Volumes can be removed from one Instance and attached to another Instance; Instance Store Volumes cannot be detached/reattached.
- EBS Volumes support full disk encryption using Amazon EBS Encyrption; Instance Store Volumes must be encrypted through the OS.

## VPC
*Question: Are EC2 instances launched in a VPC assigned sequential Private IP addresses?*

## S3 - Simple Storage Service

**Performance**

*Question:  You expect a bucket to immediately receive over 150 PUT requests per second. What should you do to ensure optimal performance?*

If the AWS workload is likely to routinely exceed 100 PUT/LIST/DELETE operations per second or 300 GET operations per second, you should avoid sequential key-names; if it will only burst to these loads, S3 will scale automatically by partitioning buckets to handle these request rates.

To avoid sequential key names, consider adding randomness as a prefix to the key-name; the randomness of the prefix more evently distributes key names across multiple index partitions.

Workloads that are GET intensive, particularly on a single object, or a small number of objects, consider using a CloudFront Distribution to cache the object, thereby reducing the load on the S3 Bucket.

**Replication Across Regions**

*Question: For HA of S3, is it possible to replicate across regions?*

AWS S3 supports Cross-Region Replication at the Bucket Level. Once enabled on a Bucket, every object uploaded will be replciated to its destination region & bucket in the configured replication region. Replication only replicates NEW or CHANGED Objects - it will not replicate current Objects in the source bucket.

The Storage Class in the source bucket (i.e. RRS), encryption state (i.e. SSE), ACL's and metadata are additionally copied during the replication.

Cross-Region Replication is built on top of S3 Object Version, which must be enabled. Additionally requires an IAM Role that can List and retrieve Objects from the source bucket and replicate to the destination bucket.

Cross-Region Replication can either copy all objects in a bucket or only those with a specific prefix.

Replication cannot occur between two buckets in the SAME Region.

**Bulk S3 Object Delete**

*Q: Max number of object that can be deleted in a single S3 bulk delete request?*

1000

**Event Notifications for S3 Buckets**

*Q: What are the possible event notifications for S3 buckets?*

New Object notifications can be triggered by S3 to one of three possible endpoints:
- SQS
- SNS
- Lambda

Object notifications are generated when new objects are created (either through PUT or POST operations, through an S3 COPY operation, after a multi-part upload completes and when an RRS Object is lost.


## CIDR Addres Blocks

*Q: What are the typical CIDR Address Blocks used by AWS, specifically the /16, /24, /26, /32 ranges?*

- /16 = 65,536 Addresses - Maximum address space of a VPC
- /24 = 256 Addresses - Typically the address space for a subnet
- /26 = 64 Addresses - Typically the address space for a subnet
- /32 = 1 Address - Address space of a single host.

## EC2 Instances

*Question: What is the difference between a Amazon PV AMI / HVM AMI*

EC2 Instances use one of two virtualization technologies - Paravirtual (PV) or Hardware Virtual Machine (HVM). Their main difference is the way in which they boot and can take advantage of special hardware (CPU, network and storage) for better performance. 

HVM uses hypervisor style interface, with the virtual machine interacting with a fully virtualized set of hardware presented by the hypervisor. HVM virtual machines can take advantage of enhanced networking and GPU processing, provided by HVM.

PV virtual machines on the other-hand run directly on hardware that does not have specific support for virtualization, but they cannot take advantage of enhanced networking and GPU processing.

All current versions of EC2 Instances support HVM as the AMI. Amazon reccommend that HVM based AMI's are used for best performance.

## IAM & Federated Identity

*Q: Read up on federated identity for IAM / AD*

If a company already manages users outside of AWS, it can use *IAM Identity Providers* instead of using IAM Users. These external users can be given permissions in an AWS Account from within the federated system. A trust relationship must be created between the Identity Provider and the AWS Account.

Typically, federated users will either assume a particular role (by being given a temporary Access Key and Secret Access Key) or perform SSO into the AWS Management Console.

One of two protocols can be used for federated identity:
- Web Identity Federation (supports OpenID Connect, e.g. Google, Amazon & Facebook) - typically used for mobile access and the federated credentials map to an AWS Role.
- SAML 2.0 based federation - Provides credential mapping to AWS Roles and to allow SSO into the AWS Console.


## VPC

*Question: What are the VPC limits?* 

http://docs.aws.amazon.com/AmazonVPC/latest/UserGuide/VPC_Appendix_Limits.html

A VPC can be created with a CIDR range between /28 (16 addresses) and /16 (65,536 addresses)

The first four addresses and the last address within a subnet are reserved by AWS and are not available for use.
