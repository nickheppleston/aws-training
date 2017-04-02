## AMAZON EMR (Elastic Map Reduce)

EMR (Elastic Map Reduce) is Amazon's managed Hadoop deployment in the Cloud. EMR manages EC2 instances within a cluster and stores data either to local storage (Instance Storage) on an HDFS file-system, or to S3 (using EMRFS).

EMR can be used for a number of applications including:
- Big Data
- Real-time Analytics (with input from Amazon Kinesis for example)
- Log File Analysis (generated from server, web or mobile applications)
- ETL style Operations (including sort aggregate and join style operations)

EMR additionally supports the deployment of common Hadoop applications and services (e.g. Pig, Hive etc.) which are pre-loaded on Hadoop AMI's.

**EMR Cluster**

An EMR cluster can easily grow and shrink depending on the demands of the cluster and/or workload.

An EMR Cluster typically contains the following node-types:
1. **A Master Node** - at most one EC2 instance of this type within a cluster.
2. **A Core Node** - runs tasks and stores data to HDFS/EMRFS; the Master Node manages Core Nodes. Can be one or more EC2 Instances. Core Nodes can be Spot Instances.
3. **Task Nodes** - Run tasks only; the Master Node manages Core Nodes. Can be one or more EC2 Instances.  Task Nodes can be Spot Instances.

**Storage Types**

- **HDFS** - the standard Hadoop file system, hosted locally on EC2 Instance Store Volumes
- **EMRFS** - an implementation of HDFS which stores cluster data on S3.



