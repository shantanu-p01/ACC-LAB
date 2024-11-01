### Step-by-Step Guide to Restore Amazon RDS DB Snapshot to S3

---

### Step 1: Create an RDS Database Instance

1. Go to **Amazon RDS** in the AWS Console.
2. Select **Databases** on the left sidebar, then click **Create database**.
3. Under **Database creation method**, select **Standard create**.

   ![RDS Creation Method - Standard Create](/docs/LAB%207%20Restore%20Amazon%20RDS%20DB%20Snapshot%20to%20S3/img/RDSCreationMethodStandardCreate.png)

4. In **Engine options**, select your preferred database engine (e.g., MySQL).

   ![RDS Engine Options - MySQL](/docs/LAB%207%20Restore%20Amazon%20RDS%20DB%20Snapshot%20to%20S3/img/RDSEngineOptionsMySQL.png)

5. Under **Templates**, choose **Free tier**.

   ![RDS Template - Free Tier](/docs/LAB%207%20Restore%20Amazon%20RDS%20DB%20Snapshot%20to%20S3/img/RDSTemplateFreeTier.png)

6. In **Settings**, specify:
    - **DB instance identifier**
    - **Master username**
    - **Master password**

   ![RDS Instance Name and Credentials](/docs/LAB%207%20Restore%20Amazon%20RDS%20DB%20Snapshot%20to%20S3/img/RDSInstanceName.png)

7. In **Connectivity**, set **Public Access** to **Yes**.

   ![RDS Connectivity - Public Access On](/docs/LAB%207%20Restore%20Amazon%20RDS%20DB%20Snapshot%20to%20S3/img/RDSConnectivityPublicAccessOn.png)

8. Click **Create database** to launch the instance.
    - Wait for the instance to be created.

   ![RDS Instance - Creating](/docs/LAB%207%20Restore%20Amazon%20RDS%20DB%20Snapshot%20to%20S3/img/RDSInstanceCreating.png)
  
   - Once the instance is successfully created, you will see it in the **Databases** list.

   ![RDS Instance - Created](/docs/LAB%207%20Restore%20Amazon%20RDS%20DB%20Snapshot%20to%20S3/img/RDSInstanceCreated.png)

---

### Step 2: Create an RDS Database Snapshot

1. Select the database instance you created.
2. Under **Actions**, choose **Take snapshot**.

   ![RDS Snapshot - Take Snapshot](/docs/LAB%207%20Restore%20Amazon%20RDS%20DB%20Snapshot%20to%20S3/img/RDSSnapshotTakeSnapshot.png)

3. Enter a name for the snapshot.

   ![RDS Snapshot - Name](/docs/LAB%207%20Restore%20Amazon%20RDS%20DB%20Snapshot%20to%20S3/img/RDSSnapshotName.png)

4. Click **Take snapshot** and wait for the snapshot to complete.

   ![RDS Snapshot - Creating](/docs/LAB%207%20Restore%20Amazon%20RDS%20DB%20Snapshot%20to%20S3/img/RDSSnapshotCreating.png)

   - Once completed, you will see the status as **Available**.

   ![RDS Snapshot - Created](/docs/LAB%207%20Restore%20Amazon%20RDS%20DB%20Snapshot%20to%20S3/img/RDSSnapshotCreated.png)

---

### Step 3: Create an S3 Bucket

1. Go to **Amazon S3** in the AWS Console.
2. Select **Buckets**, then click **Create bucket**.
3. Enter a name for your bucket.

   ![Bucket Name](/docs/LAB%207%20Restore%20Amazon%20RDS%20DB%20Snapshot%20to%20S3/img/BucketName.png)

4. Set **Object Ownership** to **ACLs disabled**.

   ![Bucket Object Ownership](/docs/LAB%207%20Restore%20Amazon%20RDS%20DB%20Snapshot%20to%20S3/img/BucketObjectOwnership.png)

5. Under **Block Public Access settings**, check **Block all public access**.

   ![Bucket Block All Public Access](/docs/LAB%207%20Restore%20Amazon%20RDS%20DB%20Snapshot%20to%20S3/img/BucketBlockAllPublicAccess.png)

6. For **Default encryption**, select **SSE-S3** and enable **Bucket Key**.

   ![Bucket Default Encryption](/docs/LAB%207%20Restore%20Amazon%20RDS%20DB%20Snapshot%20to%20S3/img/BucketDefaultEncryption.png)

7. Click **Create bucket**.

   ![Bucket Created Successfully](/docs/LAB%207%20Restore%20Amazon%20RDS%20DB%20Snapshot%20to%20S3/img/BucketCreatedSuccessfully.png)

---

### Step 4: Create an IAM Role with S3 Policy

1. In **IAM Console**, click **Roles**.
2. Click **Create role** and select **Trusted entity type** as **AWS account**.

   ![IAM Role S3 Bucket Role](/docs/LAB%207%20Restore%20Amazon%20RDS%20DB%20Snapshot%20to%20S3/img/IAMRoleS3BucketRole.png)

3. In **Add permissions**, search and attach **AmazonS3FullAccess**.

   ![IAM Role - S3 Bucket Policy Attach](/docs/LAB%207%20Restore%20Amazon%20RDS%20DB%20Snapshot%20to%20S3/img/IAMRoleS3BucketPolicyAttach.png)

4. Name the role and click **Create role**.

   ![IAM Role - Created](/docs/LAB%207%20Restore%20Amazon%20RDS%20DB%20Snapshot%20to%20S3/img/IAMRoleS3BucketRoleCreated.png)

---

### Step 5: Create a KMS Key for Encryption

1. Go to **KMS** in the AWS Console.
2. Click **Create key** and select **Symmetric** for **Key Type**.

   ![KMS Configure Key](/docs/LAB%207%20Restore%20Amazon%20RDS%20DB%20Snapshot%20to%20S3/img/KMSConfigureKey.png)

3. Add an alias for the key and assign usage permissions to the IAM role created.

   ![KMS IAM Role Selection](/docs/LAB%207%20Restore%20Amazon%20RDS%20DB%20Snapshot%20to%20S3/img/KMSIAMRoleSelection.png)

4. Click **Create key**.

   ![KMS Key Created](/docs/LAB%207%20Restore%20Amazon%20RDS%20DB%20Snapshot%20to%20S3/img/KMSKeyCreated.png)

---

### Step 6: Export the RDS Snapshot to Amazon S3

1. Go to **RDS Snapshots** in the AWS Console.
2. Select the snapshot, then click **Export to Amazon S3**.

   ![RDS Snapshot - Export to S3](/docs/LAB%207%20Restore%20Amazon%20RDS%20DB%20Snapshot%20to%20S3/img/RDSSnapshotExportToS3.png)

3. Specify the **Export identifier**, **Exported data** as **All**, and select the S3 bucket, IAM role, and KMS key.

   ![RDS Snapshot Export Settings](/docs/LAB%207%20Restore%20Amazon%20RDS%20DB%20Snapshot%20to%20S3/img/RDSSnapshotExportKMSKey.png)

---

### Step 7: Resolve Trust Relationship Error (if needed)

1. If a trust relationship error appears, go to **IAM** and select the **RDS role**.
2. In the **Trust relationships** tab, edit the policy to add:
    ```json
    "Service": "export.rds.amazonaws.com"
    ```

   ![IAM Role - Trust Policy Change](/docs/LAB%207%20Restore%20Amazon%20RDS%20DB%20Snapshot%20to%20S3/img/IAMRoleS3BucketRoleTrustPolicyChange.png)

---

### Step 8: Complete the Export

1. Return to the **RDS Export to Amazon S3** page to verify the error is resolved.
2. Click **Export to Amazon S3** and wait until the export status changes to **Complete**.

   ![RDS Snapshot Exporting and Complete](/docs/LAB%207%20Restore%20Amazon%20RDS%20DB%20Snapshot%20to%20S3/img/RDSSnapshotExportToS3Exported.png)

---

### Step 9: Verify the Exported Snapshot in S3

1. In **Amazon S3**, navigate to **Buckets** and select your RDS bucket.
2. Under **Objects**, you should see the encrypted snapshot file, confirming it was successfully exported.

   ![S3 Bucket - Snapshot Verified](/docs/LAB%207%20Restore%20Amazon%20RDS%20DB%20Snapshot%20to%20S3/img/S3BucketSnapshotVerified.png)

---