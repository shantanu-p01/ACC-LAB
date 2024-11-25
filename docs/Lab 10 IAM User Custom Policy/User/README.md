### Step-by-Step Guide for Creating an IAM role Custom Policy to access S3

---

### Step 1: Create an S3 Bucket

1. Go to the **S3** service in the AWS Console.
2. Click on **Create bucket**.
3. Enter a unique name for the bucket.
   ![S3 Bucket Name](/docs/Lab%2010%20IAM%20User%20Custom%20Policy/User/img/S3BucketName.png)
4. Click on **Create bucket** to finalize the creation.

5. Once created, navigate to the bucket and copy the ARN (Amazon Resource Name) of the S3 bucket. You'll need it in a later step.
   ![S3 Bucket ARN](/docs/Lab%2010%20IAM%20User%20Custom%20Policy/User/img/S3BucketARN.png)

---

### Step 2: Go to IAM Policies

1. Navigate to the **IAM** service in the AWS Console.
2. Click on **Policies** in the left-hand menu.

---

### Step 3: Create a New Policy

1. Click on **Create policy**.
2. In the policy creation interface, select **Service** as **S3**, since we are creating a policy for S3.
   ![Policy S3 Select](/docs/Lab%2010%20IAM%20User%20Custom%20Policy/User/img/PolicyS3Select.png)
3. Under the **List** section, check **List buckets**.
4. Under the **Read** section, check the boxes for the necessary read permissions (e.g., **GetObject**).
5. Under the **Resource** section, click on **Add ARN** and specify the ARN of the bucket:
   - Copy the ARN from the S3 bucket list if you haven't done so already.
   - Paste it in the **Add ARN** section under Resources.
   ![Add ARN's](/docs/Lab%2010%20IAM%20User%20Custom%20Policy/User/img/AddingBucketARNToPolicy.png)

---

### Step 4: Review and Create the Policy

1. Click **Next** to proceed.
2. Give the policy a name.
   ![Policy Name](/docs/Lab%2010%20IAM%20User%20Custom%20Policy/User/img/PolicyName.png)
3. Review the policy settings.
4. Click on **Create policy** to finalize the policy creation.

---

### Step 5: Create an IAM Role

1. Go to **IAM** in the AWS Console.
2. Click on **Roles** in the left-hand menu.
3. Click on **Create role**.
4. In the **Select Trusted Entity** section, select the Trusted Entity type as **AWS Service**.
   ![Role Trusted Entity](/docs/Lab%2010%20IAM%20User%20Custom%20Policy/Role/img/roleTrustedEntity.png)
5. Select **Use Case** as **EC2**.
   ![Use Case EC2](/docs/Lab%2010%20IAM%20User%20Custom%20Policy/Role/img/useCaseEC2.png)
6. Search for and select the policy you created earlier.
   ![Policy Selection](/docs/Lab%2010%20IAM%20User%20Custom%20Policy/Role/img/policySelection.png)
7. Give the role a name.
   ![Role Name](/docs/Lab%2010%20IAM%20User%20Custom%20Policy/Role/img/roleName.png)
8. Click on **Create role** to finalize the role creation.
   ![Role Created](/docs/Lab%2010%20IAM%20User%20Custom%20Policy/Role/img/roleCreated.png)

---