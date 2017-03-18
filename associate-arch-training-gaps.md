

# AWS SSA Exam - Outstanding Knowledge

## PIOPS per Volume GiB Size
*Question: Given a specific Volume GiB size (e.g. 4GiB), what is the maximum PIOPs that can be achieved (50:1 ratio)*

Provisioned IOPS (PIOPS) deliver predictable, high-performance for I/O intensive workloads such as database applications that rely on consistent and fast response times. PIOPS volumes are known as _io1_ volumes

PIOPS Volumes allow the specification of both volume size and volume performance. Multiple PIOPS volumes can be attached to an EC2 instance and striped to deliver thousands of IOPS to an application.

PIOPS Volumes range in size from 4GiB to 16TiB and between 100 - 20,000 IOPS per volume can be provisioned. The max. ration of Provisioned IOPS to requested volume size (GiB) is 50:1. A 100 GiB volume can be provisioned with up to 5,000 IOPS. Volumes greater than 400 GiB max out at 20,000 IOPS.

For more information, see the EBS Volume Types documentation at: http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EBSVolumeTypes.html

## Attaching an EBS volume across A-Z
*Question: Can an EBS volume residing in A-Z a be attached to an EC2 instance running in A-Z b?*
*Question: Can an EBS volume residing in the EU(Ireland) region be attached to an EC2 instance running in EU(London)?*

An EBS Volume is a durable, block-level storage device that can be attached to a single EC2 Instance. EBS Volumes persist independently from the lifecycle of an EC2 Instance. A volume incurs charges as long as data persists. The maximum size for an EBS Volume is 16TiB.

Data persists on the volume until the volume is explicitly deleted. After a volume is deleted, the physical block stoage used by the volume is over-written with zeroes before it is allocated to another account.

When an EBS Volume is created within an A-Z, it is automatically replicated within that zone to prevent data loss resulting from hardware failure. An EBS Volume can only be attached to an EC2 Instance __in the same A-Z__. An EBS Volume can only be attached to one EC2 Instance at a time, but multiple volumes can be attached to a single EC2 Instance.

When an instance is Terminated, an EBS Volume is automatically detached (however that behaviour can be changed if the _DeleteOnTermination_ flag is set to false through the CLI); a volume remains attached during an instance stop-start cycle.

__Encryption__

EBS Volume encryption is supported through Amazon EBS Encryption (http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EBSEncryption.html), which offers transparent block-level encryption for all EBS Volume types. EBS Encryption has minimal impact on latency and customers can expect the same level of IOPS with an encrypted volume as they would with an unencrypted volume.EBS Encryption automatically manages keys. Any snapshots created maintain the same level of encryption as the original volume, as do volumes created from those snapshots.

__Snapshots__

Snapshots of EBS Volumes (either attached to running EC2 Instances, or detached from EC2 Instances) can be taken and written to S3, where it is stored redundantly in multiple A-Z's _within the same region_. Snapshots are __incremental__ backups, meaning that only those blocks that have changed since the last snapshot are included in the latest snapshot. The Snapshot deletion process ensures that you only need to retain the most recent snapshot in order to recover the volume.

Snapshots can be created in a different Availability-Zone to the original EBS Volume, allowing a duplicate Volume to be created in that new zone. Snapshots can be shared with AWS Accounts or made public. S3 charges apply to Snapshots at the standard rate based on the amount of data stored within the snapshot.

Snapshots of encrypted EBS Volumes are also encrypted and any volume created from the snapshot will also be encrypted.

Volumes can be monitored through CloudWatch at no additional charge.

Snapshots occur asynchronously; the point-in-time snapshot is created immediately, but the snapshot is not complete until all modified blocks have been transferred to S3. A snapshot is not affected by on-going EBS reads and writes to the volume.

## EBS-Backed Instances
*Question: Which Instance Types are EBS-backed only?*

The only instance types that are all EBS-backed are the *4 series (M4, C4, R4) and the T2 series. All other series are include instance store disks.

The following EC2 Instance types are EBS-backed only:
- T2
- M4 (general purpose)
- C4 (compute optimised)
- R4 (memory optimised)

The following EC2 Instance types are _not_ EBS-backed only:
- M3 (general purpose)
- C3 (compute optimised)
- X1 (large-scale memory optimised)
- R3 (memory optimised)
- P2 (general purpose GPU compute)
- G2 (graphics optimised)
- F1 (customizable hardware acceleration)
- I3 (high I/O optimised)
- D2 (dense storage)

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

AWS S3 supports Cross-Region Replication at the Bucket Level. Once enabled on a Bucket, every object uploaded will be replciated to its destination region & bucket in the configured replication region. Replication only replicates NEW Objects uploaded - it will not replicate current Objects in the source bucket.

The Storage Class in the source bucket (i.e. RRS), encryption state (i.e. SSE), ACL's and metadata are additionally copied during the replication.

Cross-Region Replication is built on top of S3 Object Version, which must be enabled. Additionally requires an IAM Role that can List and retrieve Objects from the source bucket and replicate to the destination bucket.

Cross-Region Replication can either copy all objects in a bucket or only those with a specific prefix.

x*
*Q: Confirm the /16 /24 /26 and /32 CIDR ranges*
*Q: What is an Amazon PV AMI / HVM AMI*
*Q: What are the possible event notifications for S3 buckets???*
*Q: What is the size limit for an Instance Store Volume*
*Q: Read up on federated identity for IAM / AD*
*Q: Max number of object that can be deleted in a single S3 bulk delete request?*
