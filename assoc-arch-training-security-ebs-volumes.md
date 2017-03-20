## EBS Volumes - Overview

An EBS Volume is a durable, block-level storage device that can be attached to a single EC2 Instance. EBS Volumes persist independently from the lifecycle of an EC2 Instance. A volume incurs charges as long as data persists. The maximum size for an EBS Volume is 16TiB.

Data persists on the volume until the volume is explicitly deleted. After a volume is deleted, the physical block stoage used by the volume is over-written with zeroes before it is allocated to another account.

When an EBS Volume is created within an A-Z, it is automatically replicated within that zone to prevent data loss resulting from hardware failure. An EBS Volume can only be attached to an EC2 Instance in the same A-Z. An EBS Volume can only be attached to one EC2 Instance at a time, but multiple volumes can be attached to a single EC2 Instance.

When an instance is Terminated, an EBS Volume is automatically detached (however that behaviour can be changed if the DeleteOnTermination flag is set to false through the CLI); a volume remains attached during an instance stop-start cycle.

## EBS Volumes - Specifications

**General Purpose SSD (gp2)**
- Size Min/Max: 1 GiB / 16384 GiB
- IOPS: 3/IOPS per GiB with a minimum of 100 IOPS and max of 10,000 IOPS, burstable to 3,000 IOPS
- EBS Encryption: Yes
- Root Device (bootable): Yes

**Provisioned IOPS (io1)**
- Size Min/Max: 4 GiB / 16384 GiB
- IOPS: minimum of 100 IOPS,maximum 20,000 IOPS
- EBS Encryption: Yes
- Root Device (bootable): Yes

**Cold HDD (sc1)**
- Size Min/Max: 500 GiB / 16384 GiB
- IOPS: N/A
- EBS Encryption: Yes
- Root Device (bootable): No

**Magnetic Optimised HDD (st1)**
- Size Min/Max: 500 GiB / 16384 GiB
- IOPS: N/A
- EBS Encryption: Yes
- Root Device (bootable): No

**Magnetic**
- Size Min/Max: 1 GiB / 1024 GiB
- IOPS: N/A
- EBS Encryption: Yes
- Root Device (bootable): Yes

## PIOPS per Volume GiB Size

Provisioned IOPS (PIOPS) deliver predictable, high-performance for I/O intensive workloads such as database applications that rely on consistent and fast response times. PIOPS volumes are known as io1 volumes

PIOPS Volumes allow the specification of both volume size and volume performance. Multiple PIOPS volumes can be attached to an EC2 instance and striped to deliver thousands of IOPS to an application.

PIOPS Volumes range in size from 4GiB to 16TiB and between 100 - 20,000 IOPS per volume can be provisioned. The max. ration of Provisioned IOPS to requested volume size (GiB) is 50:1. A 100 GiB volume can be provisioned with up to 5,000 IOPS. Volumes greater than 400 GiB max out at 20,000 IOPS.

For more information, see the EBS Volume Types documentation at: http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EBSVolumeTypes.html

## Encryption

EBS Volume encryption is supported through Amazon EBS Encryption (http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EBSEncryption.html), which offers transparent block-level encryption for all EBS Volume types. EBS Encryption has minimal impact on latency and customers can expect the same level of IOPS with an encrypted volume as they would with an unencrypted volume.EBS Encryption automatically manages keys. Any snapshots created maintain the same level of encryption as the original volume, as do volumes created from those snapshots.

## Snapshots

Snapshots of EBS Volumes (either attached to running EC2 Instances, or detached from EC2 Instances) can be taken and written to S3, where it is stored redundantly in multiple A-Z's within the same region. Snapshots are incremental backups, meaning that only those blocks that have changed since the last snapshot are included in the latest snapshot. The Snapshot deletion process ensures that you only need to retain the most recent snapshot in order to recover the volume.

Snapshots can be created in a different Availability-Zone to the original EBS Volume, allowing a duplicate Volume to be created in that new zone. Snapshots can be shared with AWS Accounts or made public. S3 charges apply to Snapshots at the standard rate based on the amount of data stored within the snapshot.

Snapshots of encrypted EBS Volumes are also encrypted and any volume created from the snapshot will also be encrypted.

Volumes can be monitored through CloudWatch at no additional charge.

Snapshots occur asynchronously; the point-in-time snapshot is created immediately, but the snapshot is not complete until all modified blocks have been transferred to S3. A snapshot is not affected by on-going EBS reads and writes to the volume.

To snapshot a RAID array, use one of the following approaches:
- Pause the array and then take the snapshot
- Unmount the array and then take the snapshot
- Shutdown the EC2 Instance and then take the snapshot

## EBS Backed Instances

The only instance types that are all EBS-backed are the *4 series (M4, C4, R4) and the T2 series. All other series are include instance store disks.

The following EC2 Instance types are EBS-backed only:
- T2
- M4 (general purpose)
- C4 (compute optimised)
- R4 (memory optimised)

The following EC2 Instance types are not EBS-backed only:
- M3 (general purpose)
- C3 (compute optimised)
- X1 (large-scale memory optimised)
- R3 (memory optimised)
- P2 (general purpose GPU compute)
- G2 (graphics optimised)
- F1 (customizable hardware acceleration)
- I3 (high I/O optimised)
- D2 (dense storage)
