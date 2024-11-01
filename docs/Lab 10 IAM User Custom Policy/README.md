### Step-by-Step Guide for Creating an IAM Policy for S3 Full Access to a Specific Bucket

---

### Step 1: Create an S3 Bucket

1. Go to the **S3** service in the AWS Console.
2. Click on **Create bucket**.
3. Enter a unique name for the bucket.
   ![S3BucketName](/docs/Lab%2010%20IAM%20User%20Custom%20Policy/img/S3BucketName.png)
4. Click on **Create bucket** to finalize.

5. Once created, navigate to the bucket and copy the ARN of the S3 bucket. You'll need it in a later step.
   ![S3BucketARN](/docs/Lab%2010%20IAM%20User%20Custom%20Policy/img/S3BucketARN.png)

---

### Step 2: Go to IAM Policies

1. Navigate to the **IAM** service in the AWS Console.
2. Click on **Policies** in the left-hand menu.

---

### Step 3: Create a New Policy

1. Click on **Create policy**.
2. In the policy creation interface, select **Service** as **S3**, since we are creating a policy for S3.
   ![PolicyS3Select](/docs/Lab%2010%20IAM%20User%20Custom%20Policy/img/PolicyS3Select.png)
3. Under the **List** section, check **List buckets**.
4. Under the **Read** section, check the boxes for the necessary read permissions (e.g., **GetObject**).
5. Under the **Resource** section, click on **Add ARN** and specify the ARN of the bucket:

   - Copy the ARN from the S3 bucket list if you haven't done so already.
   - Paste it in the **Add ARN** section under Resources.
   ![Add ARN's](/docs/Lab%2010%20IAM%20User%20Custom%20Policy/img/AddingBucketARNToPolicy.png)

---

### Step 4: Review and Create the Policy

1. Click **Next** to proceed.
2. Give a name to the policy.
   ![Policy Name](/docs/Lab%2010%20IAM%20User%20Custom%20Policy/img/PolicyName.png)
3. Review the policy settings.
4. Click on **Create policy** to finalize the policy creation.

---

### Step 5: Create an IAM User and Attach the Policy

1. Go to the **Users** section in the IAM service.
2. Click on **Create user**.
3. Enter a name for the IAM user.
   ![IAMUserName](/docs/Lab%2010%20IAM%20User%20Custom%20Policy/img/IAMUserName.png)
4. Click **Next**.
5. In the **Permissions options** section, select **Attach policies directly**.
   ![IAMUserPermissionOptions](/docs/Lab%2010%20IAM%20User%20Custom%20Policy/img/IAMUserPermissionOptions.png)
6. In the **Permissions policies** section, search for the policy you just created and select it.
   ![PermissionPolicies](/docs/Lab%2010%20IAM%20User%20Custom%20Policy/img/PermissionPolicies.png)
7. Click **Next** and then **Create user**.

---

### Step 6: Generate IAM User Access Keys

1. Go to the IAM user you just created.
2. Click on **Create access key**.
   ![IAMUserAccessKeyCreation](/docs/Lab%2010%20IAM%20User%20Custom%20Policy/img/IAMUserCreateAccessKey.png)
3. Select **Command Line Interface (CLI)** as the use case.
   ![IAMAccessKeyUseCase](/docs/Lab%209%20IAM%20User%20S3%20Access/img/IAMAccessKeyUseCase.png)
4. Scroll down, check the confirmation box, and click **Next**.
   ![IAMUserUseCaseConfirmation](/docs/Lab%209%20IAM%20User%20S3%20Access/img/IAMUserUseCaseConfirmation.png)
5. Click **Create access key**.
6. Copy the **Access Key** and **Secret Access Key** and save them in a secure location.
   ![IAMAccessKeyRetrieved](/docs/Lab%209%20IAM%20User%20S3%20Access/img/IAMAccessKeyRetrived.png)

---

### Step 7: Install AWS CLI

1. Download the AWS CLI tool by clicking on [this link](https://awscli.amazonaws.com/AWSCLIV2.msi).
2. Open the installer after downloading and follow the setup steps:
   - Click **Next**.
     ![AWS-CLI-Tool-Setup1](/docs/Lab%209%20IAM%20User%20S3%20Access/img/AWS-CLI-Tool-Setup1.png)
   - Check the **License Agreement** and click **Next**.
     ![AWS-CLI-Tool-Setup2](/docs/Lab%209%20IAM%20User%20S3%20Access/img/AWS-CLI-Tool-Setup2.png)
   - Choose the default installation path or change it, then click **Next**.
     ![AWS-CLI-Tool-Setup3](/docs/Lab%209%20IAM%20User%20S3%20Access/img/AWS-CLI-Tool-Setup3.png)
   - Click **Install** to start the installation.
     ![AWS-CLI-Tool-Setup4](/docs/Lab%209%20IAM%20User%20S3%20Access/img/AWS-CLI-Tool-Setup4.png)
   - After installation completes, click **Finish**.
     ![AWS-CLI-Tool-Setup6](/docs/Lab%209%20IAM%20User%20S3%20Access/img/AWS-CLI-Tool-Setup6.png)

---

### Step 8: Configure AWS CLI with IAM Credentials

1. Open a terminal on your local machine.
2. Type the following command to configure AWS CLI:

   ```bash
   aws configure
   ```

3. Enter the **Access Key** and **Secret Access Key** obtained in Step 6, along with your **Default region** and **Default output format**.
   - Example: Use `ap-northeast-1` for the Tokyo region and `json` for output format.
   ![TerminalAWSConfigure](/docs/Lab%209%20IAM%20User%20S3%20Access/img/TerminalAWSConfigure.png)

---

### Step 9: Test Access to the S3 Bucket

1. Go back to the S3 bucket and upload a test file to it.
   ![S3BucketFileUpload](/docs/Lab%2010%20IAM%20User%20Custom%20Policy/img/S3BucketFileUpload.png)

2. In the terminal, run the following command to list the contents of your S3 bucket:

   ```bash
   aws s3 ls s3://<bucket-name>
   ```

   Replace `<bucket-name>` with your actual bucket name.
   ![TerminalAWSS3lsBucketName](/docs/Lab%2010%20IAM%20User%20Custom%20Policy/img/TerminalAWSS3lsBucketName.png)
