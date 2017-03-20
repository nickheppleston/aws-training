## EBS Volumes

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
