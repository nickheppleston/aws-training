## Route 53

- Route53 is a global service - not region specific

- When a Hosted Zone is initially created, Route53 will create SOA and NS records.

**Route53 Record Types**
Route53 supports the following record types:
- A (IPv4 Address - resolves a FQDN (or apex) to an IPv4 address)
- AAAA (IPv6 Address - resolves a FQDN (or apex) to an IPv6 address)
- SOA (Start of Authority - identities the base DNS information about the domain)
- NS (Name Server - lists the authoritative nameservers for your domain)
- PTR (Reverse IPv6)
- NAPTR
- MX
- TXT
- CNAME (Canonical Name - resolves a FQDN to another FQDN)
- SPF
- SRV

**A CNAME cannot be used as the zone apex record for a domain (e.g. modhul.com) as per the DNS spec.**

**Alias Record**
- Alias records can be mapped to the zone apex for a domain (e.g. modhul.com)
- Only used within Route53
- Alias Record lookups are free
- Very similar to a CNAME record
- Maps a FQDN to an AWS resource - e.g. ELB, Elastic Beanstalk, CloudFront or an S3 static website
- With Alias records, Route53 automatically recognises changes to the record sets that the alias resource refers to (e.g. IP Address associated with an ELB)
- If the alias points to an AWS resource (mentioned above, you cannot set a TTL)

## Route53 - Routing Policies
We Go Forward Like Soldiers (WGFLS):
- **Simple** - the default routing policy when you create a new record set; normally used when there is a single resource behind the address
- **Weighted** - routing of x% of traffic to one location and y% of traffic to another location; typically used for A/B testing.
- **Latency** - routes traffic on lowest network latency for requester; when a request is received, Route53 will select the endpoint that will give them the best response time
- **Failover** - used to create an active/passive setup; Route53 will monitor the health of an endpoint and failover if the primary is unhealthy
- **Geo-Location** - used to route traffic to a specific endpoint based on the geographic location of the user; by continent, country or US State

## Exam Tips
- ELB's do not have a pre-defined IPv4 address; instead, resolve to the ELB using the FQDN.
- Remember the difference between Alias and CNAME records - an Alias is like a CNAME, but allows you to resolve to AWS resources
- Given the choice, always choose an Alias Record over a CNAME
- Remember the Routing Policies - We Go Forward Like Soldiers (WGFLS)
