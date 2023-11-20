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
-AWS Snow family
 -- Data migration: Snowcone, Snowball Edge, Snowmobile
    Snowcone (& Snowcone SSD): Small, portable computing, anywhere, rugged & secure, withstands harsh environments.
        Snowcone: 8 tb of HDD software , Snowcone SSD- 14 TB of SSD storage
        Use AWS DataSync
    SnowBall Edge:
   <li>
       Snowaball Edge Storgae optmized : 80 tb of HDD capacity
   </li>
   <li>
       Snowaball Edge Compute optmized : 42 tb of HDD capacity or 28 tb NVMe capicity
   </li>
   
 -- Edge Computing: Snowcone, SnowBall Edge
    
