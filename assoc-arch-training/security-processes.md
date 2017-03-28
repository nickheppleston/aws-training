## Security Processes

Read the Whitepaper at: [Linky]

- AWS is responsible for the underlying infrastructure that supports the cloud; customers are responsible for anything that is put in the cloud (e.g. EC2 Instances) or connects to the cloud (VPN, Direct Connect, Internet Gateway etc.)
- AWS is responsible for security configuration, patching, A-V etc. of its products that are considered 'managed services' - Redshift, RDS, DynamoDb, Elastic Mapreduce, Workspaces etc.
- Customers are responsible for Account Management and User Access; it is recommended that MFA be implemented, communication between services is done using TLS and that user activity is logged through CloudTrail.

## Storage Decommissioning
- When a storage device has reached the end of its useful life, AWS uses a decommissioning process that is designed to prevent customer data from being exposed to unauthorized individuals.
- AWS uses the techniques described in DoD 5220.22-M or NIST 800-88 to destory data in this decommissioning process.
- All decomissioned magnetic devices are degaussed and physically destroyed.

## Network Security
- Amazon Corporate Segregation - Logically, the AWS Production network is segregated from the Amazon Corporate Network.
- AWS provides the following services including: IP Spoofing
- **IP Spoofing**: AWS host-based firewall will not permit an instance to send traffic with a source IP or MAC address other than its own.
- **Port Scans**: Unauthorized Port Scans by AWS customers are a violation of the AWS Acceptable Use Policy; however you may request permission from AWS to perform vulnerability scans as required - these scans MUST be limited to the instances you own within your account.

## AWS Credentials

Several AWS Credential types, including:
- **Passwords:** AWS Root User or IAM User Accounts to login to the AWS Console; must be minimum of 6 characters and upto 128 characters
- **MFA:** AWS Root User or IAM User Accounts to login to the AWS Console; a six-digit single-use code.
- **Access Keys:** Digitally signed requests to AWS API's (IAM Roles); includes an Access Key Id and a Secret Access Key.
- **Key Pairs:** Used to SSH/RDP into EC2 Instances / provide CloudFront signed Url's; the keys that AWS generates are 2014-bit SSH-2 RSA Keys; keys can be generated for you, or a customer can upload their own.

