### Step-by-Step Guide for Creating an IAM Policy for S3 Full Access to a Specific Bucket

---

### Step 1: Create an S3 Bucket

1. Go to the **S3** service in the AWS Console.
2. Click on **Create bucket**.
3. Enter a unique name for the bucket.
   ![S3BucketName](/docs/Lab%2010%20IAM%20User%20Custom%20Policy/User/img/S3BucketName.png)
4. Click on **Create bucket** to finalize.

5. Once created, navigate to the bucket and copy the ARN of the S3 bucket. You'll need it in a later step.
   ![S3BucketARN](/docs/Lab%2010%20IAM%20User%20Custom%20Policy/User/img/S3BucketARN.png)

---

### Step 2: Go to IAM Policies

1. Navigate to the **IAM** service in the AWS Console.
2. Click on **Policies** in the left-hand menu.

---

### Step 3: Create a New Policy

1. Click on **Create policy**.
2. In the policy creation interface, select **Service** as **S3**, since we are creating a policy for S3.
   ![PolicyS3Select](/docs/Lab%2010%20IAM%20User%20Custom%20Policy/User/img/PolicyS3Select.png)
3. Under the **List** section, check **List buckets**.
4. Under the **Read** section, check the boxes for the necessary read permissions (e.g., **GetObject**).
5. Under the **Resource** section, click on **Add ARN** and specify the ARN of the bucket:

   - Copy the ARN from the S3 bucket list if you haven't done so already.
   - Paste it in the **Add ARN** section under Resources.
   ![Add ARN's](/docs/Lab%2010%20IAM%20User%20Custom%20Policy/User/img/AddingBucketARNToPolicy.png)

---

### Step 4: Review and Create the Policy

1. Click **Next** to proceed.
2. Give a name to the policy.
   ![Policy Name](/docs/Lab%2010%20IAM%20User%20Custom%20Policy/User/img/PolicyName.png)
3. Review the policy settings.
4. Click on **Create policy** to finalize the policy creation.

---

Then go to IAM Role and Click on Create Role 
In Select Trusted Entity select the Trusted Entity Type as AWS Service
   ![roleTrustedEntity](/docs/Lab%2010%20IAM%20User%20Custom%20Policy/Role/img/roleTrustedEntity.png)
Select Use Case as EC2
   ![useCaseEC2](/docs/Lab%2010%20IAM%20User%20Custom%20Policy/Role/img/useCaseEC2.png)
Search and Select the Policy which we created earlier
   ![policySelection](/docs/Lab%2010%20IAM%20User%20Custom%20Policy/Role/img/policySelection.png)
Give a name to the Role
   ![roleName](/docs/Lab%2010%20IAM%20User%20Custom%20Policy/Role/img/roleName.png)
Then click on Create Role
   ![roleCreated](/docs/Lab%2010%20IAM%20User%20Custom%20Policy/Role/img/roleCreated.png)
