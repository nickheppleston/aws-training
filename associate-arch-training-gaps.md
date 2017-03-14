

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

An EBS Volume is a durable, block-level storage device that can be attached to a single EC2 Instance. EBS Volumes persist independently from the lifecycle of an EC2 Instance. A volume incurs charges as long as data persists. 

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

## Placement Groups
*Question: What are they, how are they used, are they cross-A-Z, cross-Region etc.*

A _Placement Group_ is a logical grouping of EC2 Instances within a single Availability-Zone. They are recommended for instances that benefit high network throughput, low network latency, or both. The instance type MUST support __Enhanced Networking__.

A Placement Group is created and then instances are launched into it. AWS recommend that instances are launched together in a single launch request and that the same Instance Type is used. An 'Insufficient Capacity Error' may be thrown if an instance is subsequently launched or if a different Instance Type is launched at a later date/time.

Placement Groups can't span multiple Availability-Zones.

There is no charge for creating a Placement Group.

## Trusted Advisor
*Question: What is it, what does it report on, what areas does it cover?*
https://aws.amazon.com/premiumsupport/trustedadvisor/

## EBS-back Instances
*Question: Which Instance Types are EBS-backed only?*

## CloudWatch
*Question: What is the minimum interval for CloudWatch metrics?*

## Consolidated Billing
*Question: What are the two different types of account?*

## EBS & Instance Store Volumes
*Question: What are the Key differences between EBS and instance-store backed volumes*
http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ComponentsAMIs.html

## VPC
*Question: Are EC2 instances launched in a VPC assigned sequential Private IP addresses?*
