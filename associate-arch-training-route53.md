## Route 53

- Route53 is a global service - not region specific

- When a Hosted Zone is initially created, Route53 will create SOA and NS records.

**SOA Record - Start of Authority**
- Identifies the base DNS information about the domain
- Includes: Host that created the domain, the admin e-mail address, a maximum TTL etc.

**NS Record - Name Server**
- Route53 always creates an NS record that has the same name as your domain
- It lists the four nameservers that are the authorative nameservers for your domain

**A Record - Address**
- Points a FQDN to an IPv4 Address

**CNAME Record - Canonical Name**
- Points to another FQDN - used to resolve one domain name to another.
- CNAME lookups incur a charge

**Alias Record**
- Only used within Route53
- Alias Record lookups are free
- Very similar to a CNAME record
- Maps a FQDN to an AWS resource - e.g. ELB, CloudFront, S3 Buckets
- With Alias records, Route53 automatically recognises changes to the record sets that the alias resource refers to (e.g. IP Address associated with an ELB)

## Route53 - Routing Policies
- Simple - the default routing policy when you create a new record set; normally used when there is a single resource behind the address
- Weighted - routing of x% of traffic to one location and y% of traffic to another location; typically used for A/B testing.
- Latency - routes traffic on lowest network latency for requester; when a request is received, Route53 will select the endpoint that will give them the best response time
- Failover - used to create an active/passive setup; Route53 will monitor the health of an endpoint and failover if the primary is unhealthy
- Geo-Location - used to route traffic to a specific endpoint based on the geographic location of the user; by continent, country or US State

## Exam Tips
- ELB's do not have a pre-defined IPv4 address; instead, resolve to the ELB using the FQDN.
- Remember the difference between Alias and CNAME records - an Alias is like a CNAME, but allows you to resolve to AWS resources
- Given the choice, always choose an Alias Record over a CNAME
- Remember the Routing Policies - We Go Forward Like Soldiers (WGFLS)
