## Security Groups - Exam Takeaways

- Security Groups are inbound DENY by default.
- Security Groups are outbound ALLOW by default.
- Changes to Security Groups are applied immediately.
- Security Groups are STATEFUL (i.e. no outbound rule is required for inbound traffic).
- An EC2 Instance can have multiple Security Groups attached.
- You cannot block specific IP Addresses, use NACL's for this purpose.
- You can specify ALLOW rules, but you cannot specify DENY rules.
