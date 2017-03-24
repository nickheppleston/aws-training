## Databases

AWS supports a number of different database tehnologies:

The AWS Relational Database Service (OLTP):
- SQL Server
- Oracle
- PostgreSQL
- MySQL
- MariaDb
- Aurora

NoSQL Databases - document based databases:
- DynamoDb
- DynamoDb supports push-button replication
- DynamoDb based on SSD
- DynamoDb supports 1. Eventual Consistency (Default) -or- Strongly Consistent Reads
- DynamoDb spread across 3 separate data-centres (not A-Z's)

Data Warehouses (OLAP):
- Redshift
- Redshift - Single Node
- Redshift - Leader + Compute Nodes
- Redshift - Charges for traffic in VPC, not outside of VPC

In-Memory Caches
- Elasticache (supporting Memcached / Redis)

## RDS

Scaling
- Can be scaled up, but need to create a snapshot and restore into a bigger database instance.
- Can be scaled out through the use of read-replicas

Automated Backups allow a database to be recovered to any point in time within the 'retention period'; The retention period can be anything between 1 - 35 days. 

Automated Backups take a daily (full) snapshot of the database and take transaction logs throughout the day. When a restore happens, RDS will restore the most recent backup and then replay the transaction logs.

Automated Backups are enabled by default and the data is stored in S3; free storage in S3 for backups upto the saize of the size of the provisioned database.

Automated Backups are taken within a defined window; during th defined window, I/O may be suspended while the data is backed-up.

Database Snapshots are manual and are retained until manually deleted; Automated Backups are deleted automatically.

Whenever an RDS database is restored from an Automated Backup or (manual) Database Snapshot, the RDS instance will have a newendpoint address

Snapshots can be copied to other S3 regions.

**Encryption**

Encryption of data at rest through KMS.

Can't enable encryption for an existing database - new new database must be created and the data migrated

## Multi-AZ & Read Replicas

Multi-AZ for disaster recovery only - sync replication
If the primary is lost, AWS automatically fails over to the secondary instance
Supported by all DB's with the exception of Aurora

Read-Replicas for read performance improvements - async replication
- Only supported by MySQL / Maria Db / PostgreSQL
- Must for Automated Backups enabled to use Read-Replicas
- Maximum of 5 Read Replicas
- Each Read-Replica will have its own endpoint address
- Read Replicas are not Multi-AZ
- Read Replicas can be promoted to become primary daabases
- Read Replicas (MySQL/MariaDb) can be deployed to a different region

## Aurora

- MySQL compatible
- Relational database engine
- Starts at 10Gb + scales in 10Gb increments
- Easy scale-up (however typically during the maintenance window)
- 2 copies of data in 3 A-Z's by default; Aurora disks are self-healing.
- Read Replicas: Aurora Replicas (max 15) / MySQL Replicas (max 5)

## Exam Tips
