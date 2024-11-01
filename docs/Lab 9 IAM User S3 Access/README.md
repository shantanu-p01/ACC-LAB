### Step-by-Step Guide for Accessing an S3 Bucket Using an IAM User

---

#### Step 1: Create an S3 Bucket

1. Go to the **Amazon S3** service in the AWS Console.
2. Click on **Create bucket**.
3. Enter a name for your bucket.
   ![S3BucketName](/docs/Lab%209%20IAM%20User%20S3%20Access/img/S3BucketName.png)
4. Click **Create bucket** to complete the setup.

---

#### Step 2: Create an IAM User with S3 Access

1. Navigate to the **IAM** service in the AWS Console.
2. In the left-hand panel, under **Access Management**, click **Users**.
   ![IAMUserName](/docs/Lab%209%20IAM%20User%20S3%20Access/img/IAMUserName.png)
3. Click **Next**.
4. In the **Permission options** section, select **Attach policies directly**.
   ![IAMPermissionsOptions](/docs/Lab%209%20IAM%20User%20S3%20Access/img/IAMPermissionsOptions.png)
5. In the **Permission policies** section, search for `AmazonS3FullAccess` and select it.
   ![IAMPermissionPolicies](/docs/Lab%209%20IAM%20User%20S3%20Access/img/IAMPermissionPolicies.png)
6. Click **Next** and then **Create user** to finalize the user creation.
   ![IAMUserCreationSuccess](/docs/Lab%209%20IAM%20User%20S3%20Access/img/IAMUserCreationSuccess.png)

---

#### Step 3: Create Access Keys for the IAM User

1. Go to the user you just created.
2. Click on **Create access key**.
   ![IAMUserAccessKeyCreation](/docs/Lab%209%20IAM%20User%20S3%20Access/img/IAMUserAccessKeyCreation.png)
3. Select **Command Line Interface (CLI)** as the use case.
   ![IAMAccessKeyUseCase](/docs/Lab%209%20IAM%20User%20S3%20Access/img/IAMAccessKeyUseCase.png)
4. Scroll down, check the confirmation box, and click **Next**.
   ![IAMUserUseCaseConfirmation](/docs/Lab%209%20IAM%20User%20S3%20Access/img/IAMUserUseCaseConfirmation.png)
5. Click **Create access key**.
6. Copy the **Access Key** and **Secret Access Key** and save them in a secure location.
   ![IAMAccessKeyRetrived](/docs/Lab%209%20IAM%20User%20S3%20Access/img/IAMAccessKeyRetrived.png)

---

#### Step 4: Install AWS CLI

1. Download the AWS CLI tool by clicking on [this link](https://awscli.amazonaws.com/AWSCLIV2.msi).
2. After downloading, open the installer and follow the setup steps.
   - Click **Next**.
     ![AWS-CLI-Tool-Setup1](/docs/Lab%209%20IAM%20User%20S3%20Access/img/AWS-CLI-Tool-Setup1.png)
   - Check the **License Agreement** and click **Next**.
     ![AWS-CLI-Tool-Setup2](/docs/Lab%209%20IAM%20User%20S3%20Access/img/AWS-CLI-Tool-Setup2.png)
   - Choose the default installation path or change it, then click **Next**.
     ![AWS-CLI-Tool-Setup3](/docs/Lab%209%20IAM%20User%20S3%20Access/img/AWS-CLI-Tool-Setup3.png)
   - Click **Install** to begin the installation.
     ![AWS-CLI-Tool-Setup4](/docs/Lab%209%20IAM%20User%20S3%20Access/img/AWS-CLI-Tool-Setup4.png)
   - Wait for the installation to complete, then click **Finish**.
     ![AWS-CLI-Tool-Setup6](/docs/Lab%209%20IAM%20User%20S3%20Access/img/AWS-CLI-Tool-Setup6.png)

---

#### Step 5: Configure AWS CLI with IAM Credentials

1. Open a terminal on your local machine.
2. Enter the following command to configure AWS CLI:

   ```bash
   aws configure
   ```

3. When prompted, enter the **Access Key** and **Secret Access Key** obtained in Step 3, as well as your **Default region** and **Default output format**.
   - Example: Use `ap-northeast-1` for the Tokyo region and `json` for output.
   ![TerminalAWSConfigure](/docs/Lab%209%20IAM%20User%20S3%20Access/img/TerminalAWSConfigure.png)

---

#### Step 6: Upload Files to the S3 Bucket

1. Go to the **Amazon S3** service in your browser.
2. Navigate to your bucket and upload any file.
   ![S3UploadSomething](/docs/Lab%209%20IAM%20User%20S3%20Access/img/S3UploadSomething.png)

---

#### Step 7: Access S3 Bucket Contents Using AWS CLI

1. In the terminal, use the following command to list all buckets:

   ```bash
   aws s3 ls
   ```

   This will display the buckets you currently have.
   ![TerminalAWSS3ls](/docs/Lab%209%20IAM%20User%20S3%20Access/img/TerminalAWSS3ls.png)

2. To view the contents of a specific bucket, use the command below, replacing `<bucket-name>` with the name of your bucket:

   ```bash
   aws s3 ls s3://<bucket-name>
   ```

   ![TerminalAWSS3lsBucketName](/docs/Lab%209%20IAM%20User%20S3%20Access/img/TerminalAWSS3lsBucketName.png)
