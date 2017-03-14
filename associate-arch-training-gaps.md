

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

## Placement Groups
*Question: What are they, how are they used, are they cross-A-Z, cross-Region etc.*

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
