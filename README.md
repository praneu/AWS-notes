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
    on the bucket is going to be blocked.
