## What to know for the Exam

Know the differences between:
- On Demand
- Spot (remember that if *you* terminate you pay; if AWS terminate, you don't pay for that hour)
- Reserved
- Dedicated Hosts

EC2 Instance Types
- DR MC GIFT PX

EBS Volume Types:
- SSD, General Purpose (GP2) - up-to 10,000 IOPS [BOOT]
- SSD, Provisioned IOPS (IO1) - up-to 20,000 IOPS [BOOT]
- HDD, Throughput Optimized (ST1) - frequently accessed sequential data [NO BOOT]
- HDD, Cold (SC1) - less frequently accessed data (e.g. file server) [NO BOOT]
- HDD, Magnetic - cheap infewquently accessed storage [BOOT]

EBS Volume can only be attached to a single EC2 Instance at any one time.

Termination Protection is disabled by default

The Root EBS Volume will be deleted on termination by default BUT other attached EBS Volumes will not.

Root Volumes cannot be encrypted by default (use an OS or user app for encryption), but other Volumes can be using EBS Encryption

Volumes exist on EBS / Snapshots live on S3 (single region, multi A-Z) / Snapshots are point in time and incremental.

Snapshots of encrypted volumes are encrypted automatically / volumes restored from an encrypted snapshot are encrypted

Snapshots can be shared, but only if they are encrypted (KMS Keys can't be shared)

Stop an instance before taking a Snapshot that will be used a a root device.

EC2 Instances with Instance Store Volumes CANNOT be stopped / EBS backed instances CAN be stopped / both can be rebooted without losing data

To take a snapshot of a RAID array (we need to stop I/O on a RAID array to make it application consistent):
- Unmount the drive
- Freeze the filesystem
- Shutdown the associated EC2 instance

AMI's are regional / can be copied to other regions

CloudWatch
- Standard monitoring 5 mins / Detailed monitoring 1 min (pay extra)
- For performance monitoring, not auditing (use CloudTrail for auditing)
- Create alarms for auto scaling
- Events allow you to respond to state changes within your resources
- Logs - logs can be pushed to CloudWatch to allow aggregation, monitoring and storing

IAM Roles can be assigned to an EC2 instance, but only using the command line.
IAM Roles are global - they can be used in any region.

Instance Meta-Data - used to get an meta-data from an instance, on the instance
 - http://169.254.169.254/latest/meta-data/
 - no such thing as user-data for an instance
 
 EFS - supports NFSv4
 EFS - no need to pre-provision and only pay for storage that is used
 EFS - can support thousands of multiple connections
 EFS - data is stored across multiple A-Z's within a region
 EFS - read AFTER write consistency
