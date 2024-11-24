### Step-by-Step Guide for Accessing S3 Objects using AWS CloudFront

---

#### 1. Create an S3 Bucket

1. Go to the **S3 Service** and click on **Create Bucket**.
2. Provide a **unique name** for the S3 bucket.

   ![S3 Bucket Name](/docs/Lab%2012%20Access%20S3%20Objects%20using%20AWS%20CloudFront/img/s3BucketName.png)

3. Click on **Create Bucket**.
4. Navigate to the S3 bucket you just created and upload your `index.html` file. [Click here](/docs/Lab%2012%20Access%20S3%20Objects%20using%20AWS%20CloudFront/index.html) to download the `index.html` file.

   ![S3 File Uploaded](/docs/Lab%2012%20Access%20S3%20Objects%20using%20AWS%20CloudFront/img/s3FileUploaded.png)

#### 2. Set Up CloudFront Distribution

1. Go to the **CloudFront Service** and click on **Create Distribution**.

   ![CloudFront Create Distribution](/docs/Lab%2012%20Access%20S3%20Objects%20using%20AWS%20CloudFront/img/cFCreateDist.png)

2. In the **Origin Domain** section, select the S3 bucket you just created.

   ![CloudFront Origin Domain](/docs/Lab%2012%20Access%20S3%20Objects%20using%20AWS%20CloudFront/img/cFOriginDomain.png)

3. In the **Origin Access** section, select the **Origin access control settings** and choose your S3 bucket in the **Origin access control field**.

   ![CloudFront Origin Access](/docs/Lab%2012%20Access%20S3%20Objects%20using%20AWS%20CloudFront/img/cFOriginAccess.png)

4. Ignore all other settings and scroll down to the **Web Application Firewall (WAF)** section. Select **Do not enable security protections**.

   ![CloudFront WAF](/docs/Lab%2012%20Access%20S3%20Objects%20using%20AWS%20CloudFront/img/cFWAF.png)

5. In the **Settings** section, locate the **Default Root Object** field. Enter the name of the file you uploaded to the S3 bucket (e.g., `index.html`).

   ![CloudFront Default Root Object](/docs/Lab%2012%20Access%20S3%20Objects%20using%20AWS%20CloudFront/img/cFDefaultRootObjectField.png)

6. Click on **Create Distribution**.
7. After the distribution is created, click on the **Copy Policy** button.

   ![CloudFront Distribution](/docs/Lab%2012%20Access%20S3%20Objects%20using%20AWS%20CloudFront/img/cFDistCreated.png)

#### 3. Update S3 Bucket Policy

1. Go back to your S3 bucket.

   ![S3 Bucket](/docs/Lab%2012%20Access%20S3%20Objects%20using%20AWS%20CloudFront/img/s3Buck.png)

2. Navigate to the **Permissions** tab.

   ![S3 Permissions](/docs/Lab%2012%20Access%20S3%20Objects%20using%20AWS%20CloudFront/img/s3Perm.png)

3. Scroll down to the **Bucket Policy** section and click on the **Edit** button.
4. Paste the bucket policy you copied earlier from CloudFront.

   ![S3 Bucket Policy](/docs/Lab%2012%20Access%20S3%20Objects%20using%20AWS%20CloudFront/img/s3BuckPolicy.png)

5. Click on **Save Changes**.

   ![S3 Bucket Policy Changes Saved](/docs/Lab%2012%20Access%20S3%20Objects%20using%20AWS%20CloudFront/img/s3PolicyChangesSaved.png)

#### 4. Test the Configuration

1. Go back to your CloudFront distribution and copy the **Distribution Domain Name**.

   ![CloudFront Distribution URL](/docs/Lab%2012%20Access%20S3%20Objects%20using%20AWS%20CloudFront/img/cFDistURL.png)

2. Paste the domain name into a new browser tab.
3. You should see the webpage working as expected.

   ![WebPage Works](/docs/Lab%2012%20Access%20S3%20Objects%20using%20AWS%20CloudFront/img/webPageWorks.png)

#### Done!

