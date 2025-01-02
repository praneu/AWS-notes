# EC2 Instances 
- On demand instances<br>
 -- Short term and un-interrupted workloads.
- Reserved instances <br>
 -- Long term work load
 -- Reserved Instance’s Scope – Regional or Zonal
- Spot instances <br>
 --  short workloads, cheap, can lose instances (less reliable)
 --  MOST cost-efficient instances
 -- Useful for workloads that are resilient to failure like batch jobs, data analysis, image processing
- Dedicated hosts
 -- compliance requirements and use your existing server-bound software license
- Dedicated Instances
 -- pay, by the hour, for instances that run on single-tenant hardware
- On-Demand Capacity Reservations <br>
  -- Suitable for short-term, uninterrupted workloads that needs to be in a specific AZ.


# AWS-notes-S3 security

# S3 Encryption
- Server-Side Encryption(SSE) <br>
--Server-Side Encryption with Amazon S3-Managed Keys (SSE-S3)
    Header must be set to Must set header "x-amz-server-side-encryption": "AES256" to enable the encryption
    This is enabled by default for sew buckets and objects.
--Server-Side Encryption with KMSKeys Stored in AWS KMS (SSE-KMS)
     KMS= Key Management Service
     KMS keeps all the logs in AWS cloudTrail which helps in to audit keys.
     Having a very, very high throughput S3 bucket,and  encrypting everything using 
     KMS keys, may go into a thread link kind of use case.
--Server-Side Encryption with Customer-Provided Keys(SSE-C)
     SSE-C is managed by customer outside AWS.
     But Amazon S3 will never store the encryption key provided.After they're 
     used, they're being discarded.
     HTTPS must be used
- Client-Side Encryption
    The idea with client-side encryptionis that the clients must encrypt data 
    themselvesbefore sending data to Amazon S3. The decryption of the data 
    happens on the client outside of Amazon S3.
    Customer fully manages the keys and encryption cycle. <br>
- Encryption in transit(SSL/TLS)
    Encryption in flight is also called SSL/TLS.
    HTTPS is mandatory for SSE-C <br>
- Forcing encryption in Transit aws: Secured transport
    By using a bucket policy. Attach a bucket policy with the S3 
    bucket, and attach the statement saying to deny an object 
    GetObject operation in the condition is 
    "aws:SecureTransport":"False".
    So SecureTransport is going to be true whenever using HTTPS
    and false whenever not using an encryption,
    an encrypted connection,
    and so, therefore, any user trying to use HTTP
    on the bucket is going to be blocked.<br>
# S3 CORS
-- CORS= Cross ORiginal Resource Sharing
     Web Browser based mechanism of security to allow or deny requests to other origins while 
     visiting the main origin.
     The requests won’t be fulfilled unless the other origin allows for the 
     requests, using CORS Headers (also called the Access-Control-Allow-Origin)
-- S3 Access log
      S3 Access log are use to access the logs from any account. Any request made will be authozized or 
      denied will be logged into the S3 Bucket.
      Do not set the logging bucket to be the monitor bucket as is creates a logging loop growing the bucket 
      exponentially. <br>
# Advanced Storage on AWS
- AWS Snow family
 - Data migration: Snowcone, Snowball Edge, Snowmobile <br>
    Snowcone (& Snowcone SSD): Small, portable computing, anywhere, rugged & secure, withstands harsh environments.
        Snowcone: 8 tb of HDD software , Snowcone SSD- 14 TB of SSD storage
        Use AWS DataSync <br>
    SnowBall Edge:
       Snowaball Edge Storgae optmized : 80 tb of HDD capacity
       Snowaball Edge Compute optmized : 42 tb of HDD capacity or 28 tb NVMe capicity <br>

   Snowmobile : Transfer data greater than 100 PB, high security, better than snowball<br>
   
 - Edge Computing: Snowcone, SnowBall Edge
     Snowcone & snowcone SSD: 
      2 CPUs, 4 GB of memory, wired or wireless access
      USB-C power using a cord or the optional battery <br>
     Snowball Edge- Compute Optimized: 
       104 vCPUs, 416 GiB of RAM
       Optional GPU
       Storage Clustering available (up to 16 nodes) <br>
      Snowball Edge - Storage optimized:
        Up to 40 vCPUs, 80 GiB of RAM, 80 TB storage
        Long-term deployment options: 1 and 3 years discounted pricing <br>

 - AWS OpsHub
      a software you install on your computer / laptop to manage your Snow Family Device <br>

 -- Snowball into Glacier : Snowball cannot be import to glacier directly, it must use Amazon S3 first, in combination with an S3 lifecycle policy

 - Amazon FSX
   -- Launch 3rd party high-performance file systems on AWS and is a fully managed services.<br>

   FSX for Windows file server: Fully managed Windows file system share driv, Can be mounted on Linux EC2 instances, Supports Microsoft's Distributed File System (DFS) Namespaces.
                                Has both SSD and HDD for storage option. Can be accessed from on-permises infastructure, configured to be multi AZ, daily data backup to S3 bucket.
   FSX for Luster: Lustre is a type of parallel distributed file system, for large-scale computing. Used for Machine Learning, High Performance Computing (HPC). Has seamless intrgration eith S3
                   and Can be used from on-premises servers (VPN or Direct Connect).<br>
      File system distribution:
           Scratch file system: Temporary storage, Data is not replicated, Usage: short-term processing, optimize costs
           Persistant file system: Long-term storage, Data is replicated within same AZ, Usage: long-term processing, sensitive data. <br>
           
   FSX for NetApp ONTAP: Managed NetApp ONTAP on AWS, File System compatible with NFS, SMB, iSCSI protocol, Point-in-time instantaneous cloning (helpful for testing new workloads).

 FSX for OpenZFS: File System compatible with NFS (v3, v4, v4.1, v4.2), Point-in-time instantaneous cloning (helpful for testing new workloads).
 
- Amazon EFS provides a file system interface, file system access semantics (such as strong consistency and file locking), and concurrently accessible storage for up to thousands of Amazon EC2 instances. EFS provides the performance, durability, high availability, and storage capacity needed by the 1000 Linux servers.
- ALB, ELB, NLB & their Difference
If your application is composed of several individual services, an Application Load Balancer can route a request to a service based on the content of the request, such as Host field, Path URL, HTTP header, HTTP method, Query string, or Source IP address.
ALB: HTTP/HTTPS
NLB: TCP, UDP, TLS
CLB: TCP, SSL/TLS,  HTTP/HTTPS

- Sticky Sessions (also known as session affinity) is an option you can enable in an ALB. When enabled, this causes traffic to be routed to the same EC2 instance based on the client session. 

- CloudWatch and its Metrics
Cloudwatch has CPU Utilization, Network Utilization, and Disk Reads activities. Metrics not readily available in CloudWatch, such as memory utilization, disk space utilization, and many others, can be collected by setting up a custom metric.

- AWS CloudTrail → Aditing purposes
AWS CloudTrail is a service that enables governance, compliance, operational auditing, and risk auditing of your AWS account
AWS CloudTrail increases visibility into your user and resource activity by recording AWS Management Console actions and API calls.
By default, CloudTrail event log files are encrypted using Amazon S3 server-side encryption (SSE)

- Cloudfront is a content delivery network.
In CloudFormation, a template is a JSON or a YAML-formatted text file that describes your AWS infrastructure. Templates include several major sections. The Resources section is the only required section.

- Amazon API Gateway: Mostly used for serverless architecture.

- Dynamo DB and DB Stream
Amazon DynamoDB is not capable of handling complex queries and highly transactional (OLTP) workloads.
 - Amazon Aurora
Aurora includes a high-performance storage subsystem. Aurora also automates and standardizes database clustering and replication, which are typically among the most challenging aspects of database configuration and administration.
- Amazon Redshift
Used for Data warehousing purposes to build analytics workloads and supports petabytes of data and tens and millions of requests per minute. Redshift cluster does not create secondary replicas in the management console. DR can be done through snapshots and restored to another region. 

- Amazon Quantum Ledger Database (Amazon QLDB) is a fully managed ledger database that provides a transparent, immutable, and cryptographically verifiable transaction log owned by a central trusted authority. Amazon QLDB can be used to track every application data change and maintain a complete and verifiable history of changes over time.

 - Although you can use AWS DataSync to automate and accelerate data transfer from on-premises to AWS, it’s not capable of replicating existing applications running on your server.

- AWS Local Zones are a type of AWS infrastructure deployment that places compute, storage, database, and other select services closer to large population, industry, and IT centers, enabling you to deliver applications that require single-digit millisecond latency to end-users.

- ASG
Target tracking scaling – Increase or decrease the current capacity of the group based on a target value for a specific metric. This is similar to the way that your thermostat maintains the temperature of your home – you select a temperature and the thermostat does the rest.
Step scaling – Increase or decrease the current capacity of the group based on a set of scaling adjustments, known as step adjustments, that vary based on the size of the alarm breach.
Simple scaling – Increase or decrease the current capacity of the group based on a single scaling adjustment.


- EFA (Elastic Fiber Adapter): network device that you can attach to your EC2 instance to significantly accelerate machine learning applications and High-Performance Computing (HPC).

- Fault Tolerance is the ability of a system to remain in operation even if some of the components used to build the system fail. In AWS, this means that in the event of server fault or system failures, the number of running EC2 instances should not fall below the minimum number of instances required by the system for it to work properly. So if the application requires a minimum of 4 instances, there should be at least 4 instances running in case there is an outage in one of the Availability Zones or if there are server issues.

- AWS Control Tower offers a straightforward way to set up and govern an AWS multi-account environment, following prescriptive best practices. AWS Control Tower orchestrates the capabilities of several other AWS services, including AWS Organizations, AWS Service Catalog, and AWS Single Sign-On, to build a landing zone in less than an hour. 

- Cloudwatch: You can create alarms that automatically stop, terminate, reboot, or recover your EC2 instances using Amazon CloudWatch alarm actions.
RAID 0 configuration enables you to improve your storage volumes’ performance by distributing the I/O across the volumes in a stripe.
RAID 1 configuration is used for data mirroring.

- AWS CloudFormation provides a common language for you to describe and provision all the infrastructure resources in your cloud environment.

- Amazon Elastic Kubernetes Service (Amazon EKS)
The Kubernetes Horizontal Pod Autoscaler automatically scales the number of Pods in a deployment, replication controller, or replica set based on that resource’s CPU utilization.
Amazon EKS supports two autoscaling products:
-- Cluster Autoscaler
The Kubernetes Cluster Autoscaler automatically adjusts the number of nodes in your cluster when pods fail or are rescheduled onto other nodes. The Cluster Autoscaler uses Auto Scaling groups. <br>
-- Karpenter
Karpenter is a flexible, high-performance Kubernetes cluster autoscaler that launches appropriately sized compute resources, like Amazon EC2 instances, in response to changing application load. It integrates with AWS to provision compute resources that precisely match workload requirements.

- Amazon SQS
Amazon SQS uses short polling by default, querying only a subset of the servers (based on a weighted random distribution) to determine whether any messages are available for inclusion in the response.
-- Short polling works for scenarios that require higher throughput
-- Long polling helps reduce your cost of using Amazon SQS by reducing the number of empty responses when there are no messages available. Long polling eliminates false empty responses by querying all (rather than a limited number) of the servers. Long polling returns messages as soon any message becomes available.

- AWS Storage Gateway is a set of hybrid cloud services that gives you on-premises access to virtually unlimited cloud storage. 
- AWS DataSync is an online data transfer service that simplifies, automates, and accelerates moving data between on-premises storage systems and AWS Storage services, as well as between AWS Storage services.
- AWS Storage Gateway is more suitable for integrating your storage services by replicating your data, while AWS DataSync is better for workloads that require you to move or migrate your data.
- Amazon FSx for Lustre provides a high-performance file system optimized for fast processing of workloads such as machine learning, high-performance computing (HPC), video processing, financial modeling, and electronic design automation (EDA).
- Access keys are long-term credentials for an IAM user or the root user of an AWS account. You can use access keys to sign programmatic requests to the AWS CLI or AWS API (directly or using the AWS SDK).
- Lambda function URLs are HTTP(S) endpoints dedicated to your Lambda function. You can easily create and set up a function URL using the Lambda console or API. Once created, Lambda generates a unique URL endpoint for your use.
- By default, records of a stream in Amazon Kinesis are accessible for up to 24 hours from the time they are added to the stream. You can raise this limit to up to 7 days by enabling extended data retention.
- An egress-only Internet gateway (IPV6)is a horizontally scaled, redundant, and highly available VPC component that allows outbound communication over IPv6 from instances in your VPC to the Internet and prevents the Internet from initiating an IPv6 connection with your instances.
- Amazon Inspector is a vulnerability management service that continuously scans your AWS workloads for vulnerabilities. Amazon Inspector automatically discovers and scans Amazon EC2 instances and container images residing in Amazon - Elastic Container Registry (Amazon ECR) for software vulnerabilities and unintended network exposure.
- AWS Transit gateway can be attached to VPC, VPN, Peering connection, and direct connect gateway. 
- AWS Xray is used to trace your application when you execute it. 
- Workload discovery on AWS is a tool specifically used for maintaining an inventory of the AWS resources across your accounts' various regions and mapping relationships between them, and displaying them in a web UI.
- AWS Firewall Manager: Manage rules in all accounts of an AWS Organization. AWS WAF Protects your web applications from common web exploits(SQL injection, DDoS).
- AWS Direct Connect connection has low latency and is connected through private internet, which is better as compared to AWS site-to-site VPN connection (uses public internet & low latency)
- RDS DB failover needs a resilient solution to reduce failover: → RDS proxy because RDS proxy maintains a poll of warm db connections during a failover, the proxy automatically reestablishes connections to the new primary db, minimizing the impact on an application’s availability and reducing timeouts. RDS Reas replicas cannot use these failovers, which are used to improve read scalability and enable performance.
- AWS Budgets is ideal for setting cost or usage limits, providing proactive alerts via email or SNS when thresholds are approached or exceeded. It focuses on budgeting and forward-looking control with limited visualization. 
- AWS Cost Explorer, on the other hand, offers detailed cost and usage analysis, rich visualizations, and granular insights into services, regions, and tags. While it excels in identifying trends and optimization opportunities, it lacks the proactive notifications of Budgets. Together, they allow you to monitor spending proactively with Budgets and analyze costs in depth using Cost Explorer.
- Use AWS Budgets to set cost limits and receive alerts when spending is near the threshold.
- Use AWS Cost Explorer to analyze the root cause of unexpected costs and adjust usage patterns or optimize resources.
- AWS Kinesis Data Firehose focuses on delivering data towards a destination like S3 primarily for batch analysis. 
- Files are rarely accessed: Glacial retrieval, Infrequently: Infrequent access, No pattern to access the file: Intelligent tiering, Frequent access: S3 standard.
- Amazon elastic cache is primarily used for in-memory caching useful for Dynamic content.
