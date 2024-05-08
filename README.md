**Welcome to the implementation of the Term_Paper for TDC:** <br>
  Here i will be explaining the steps that i used to implement various innovations in distributed cloud storage as mentioned in the Term Paper: <br><br>
    1. **Object Storage**: <br>
      i) In the AWS management console select services and select S3 from the drop down list. <br>
      ii) Select buckets and create a bucket. Now choose the bucket name, region for the bucket, uncheck block public access then click on create bucket.(because we need this bucket to be publicly available) <br>
      iii) Now in the S3 console, select the created bucket upload the data which you want to display and update the bucket policy with the following code to enable public_read_access. <br>
      iv) The bucket is now created with a public read access to all users, the link to access the data in the created bucket will be mentioned in the links.txt in this repo. 
      
       code - 
       {
       "Version": "2012-10-17",
       "Statement": [
         {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::objectstimp/*"
        }
      ]
    }
<br>

   **2. Metadata Management:** <br>
     i) Create a S3 bucket similar to the above mentioned steps. <br>
     ii) Create a AWS Glue Data Catalog to catalog metadata information about the data stored in S3 bucket. <br>
     iii) In the AWS Glue Catalog select Databases, then add database give the name for the database and click on create database. <br>
     iv) Now add click on Add tables using crawlers, select S3 as datasource. <br>
     v) Choose the datasource link (e.g-s3 bucket link), choose how many times the crawler should run or how it should run based on the requirements. <br>
     vi) Review and crawler config and click finish. <br>
     vii) The crawler is now created and we can run the crawler manually, whenever the crawler is executed the metadata about the files stored in the s3 bucket will be updated into a AWS Athena Tables. <br>
     viii) We can now write queries to retrieve the data from the Athena. <br>
     ix) The output can be seen in the file Metadata_implementation_op image where you can see the logs that the crawler is updating the data to the database table that we created in AWS Glue. <br>

  **3. Data Tiering and Caching** <br>
    i) Create a S3 bucket with the data in it. <br>
    ii) In the S3 management console, select the S3 bucket. <br>
    iii) Go to management tab and click on create lifecycle rule, now create a lifecycle rule based on last access date. The condition used in code is access_date > 30. If this condition is saltisfied we 
    select S3 Intelligent_tiering storage. <br>
    iv) Now create AWS CloudFront distribution to cache content from the S3 bucket, improvig access speed and latency.<br>
    v) give the name for the distribution and choose "web" delivery method, set S3 bucket as origin.<br>
    vi) Define the behaviors such as Time-To-Live, cache control header, etc. <br>
    vii) Click create, now CloudFront Distribution for the content is created. Use the link in the distribution to access the data via CloudFront. <br>
    viii) In this way Data Tiering is implemented using S3 buckets in AWS and Caching is implemented using CloudFront in AWS.<br>
    ix) In the file called CacheStatistics_Timestamp we can see that how many page hits are done and the time of the hits and various other statistics. <br>


**NOTE : The code for the bucket policy is different for all the three implementations in S3 because there is a combination of various services used. I have given the code for Object storage implementation as an example.
**    
     
