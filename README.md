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

 -- <b>Snowball into Glacier</b>: Snowball cannot be import to glacier directly, it must use Amazon S3 first, in combination with an S3 lifecycle policy

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

   
     
