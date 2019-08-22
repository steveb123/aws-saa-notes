# My notes from the acloud.guru AWS Solutions Architect Associate course
## (mainly just a copy of the "Exam Tips" at the end of each chapter)

# IAM and S3
## IAM
Consists of:  
- Users  
- Groups  
- Roles  
- Policies  

IAM is:  
- Universal, does not apply to specific regions  
- New users have no permissions when first created
- New users are assigned access key id and secret access keys when first created
- Access keys are used to access AWS programmatically
- Can only view the keys once, they need to be regenerated if lost

## S3
- Object based storage (not block based, so unable to store operating systems, databases, etc)
- Files can be 0 bytes to 5TB
- The largest object that can be uploaded in a single PUT is 5 gigabytes. For objects larger than 100 megabytes, customers should consider using the Multipart Upload capability
- Unlimited storage
- Files are stored in buckets
- Bucket names must be unique
- Buckets are private by default, policies and access control lists are used to configure access
- Can be configured for access logs
- Read after write consistency for PUTS of new objects
- Eventual consistency for overwrite PUTS and DELETES (can take time to propagate)

### S3 Storage Classes
#### S3 Standard
- 99.99% availability
- 99.999999999% durability
- Can sustain loss of two facilities concurrently

#### S3 - IA
- Infrequently accesses
- Costs less than S3, but there is a retrieval fee

#### S3 One Zone - IA
- Lower cost that S3 - IA
- Single availability zone
- 99.50% availability

#### S3 - Intilligent Tiering
- Designed to optimise costs by automatically moving data to the most cost effective tier without performance impact.

#### S3 Glacier
- Low cost archiving
- Retrieval times configurable from minutes to hours

#### Glacier Deep Archive
- Lowest cost storage (archive)
- Longest retrieval time

### Encryption
- Encryption is in transit is achieved by SSL/TLS
- Encryption at rest is achieved with:
  - S3 managed keys
  - AWS key management service
  - Server side encryption with customer provided keys
  - Client side encryption

### Cross Region Replication
- Versioning must be enabled at source and destination buckets
- Regions must be unique
- Files in an existing bucket are not replicated automatically
- All subsequent updated files will be replicated automatically
- Delete markers are not replicated

### Lifecycle Policies
- Automates moving objects between different storage tiers
- Can be used with versioning
- Can be applied to current and previous versions

### S3 Transfer Accelleration
- Improves speed and performance

### CloudFront
#### Components
- Edge location. The location where content will be cached, separate to an AWS region
- Origin. Origin of the files that the CDN will distribute. Could be S3 bucket, EC2 instance, ELB or Route53
- Distribution. The name of the CDN which contains a list of the edge locations
- Web distribution. Used for websites

####
- Edge locations are read/write
- Objects are cached for the life of the TTL
- You can clear caches objects, but you will be charged

### Snowball
- Large disk used to transfer data to/from AWS
- Can import/export data to S3

### Storage Gateway
- File Gateway. For flat files stored directly on S3 (NFS)
- Stored Volumes. Entire dataset is stored on site and is asynchronosouly backed up to S3
- Cached Volumes. Entire dataset is stored on S3 and frequently accessed data is cached on site.
- Virtual Tape Library. Used for backup (uses applicaitons like NetApp, Veeam, Bakup Exec)

S3 FAQs are useful: https://aws.amazon.com/s3/faqs/
