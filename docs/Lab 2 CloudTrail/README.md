### **Lab 2: AWS CloudTrail with CloudWatch and SNS – Detailed Step-by-Step Guide**

---

### **Step 1: Create an S3 Bucket for CloudTrail Logs**

1. **Open the S3 Management Console**:
   - Navigate to AWS S3 Console.

2. **Create a New Bucket**:
   - Click on **Create Bucket**.
   - Give your bucket a name (e.g., `acc-ty-1113`).
   ![BucketName](/docs/Lab%202%20CloudTrail/img/BucketName.png)
   
3. **Enable Bucket Versioning**:
   - In the **Bucket Versioning** section, enable versioning. This ensures that multiple versions of logs are retained.
   ![BucketVersioning](/docs/Lab%202%20CloudTrail/img/BucketVersioning.png)
   
4. **Complete Bucket Creation**:
   - Keep all other settings at default, and click **Create Bucket** to finish.
   ![BucketCreatedSuccessfully](/docs/Lab%202%20CloudTrail/img/BucketCreatedSuccessfully.png)

---

### **Step 2: Set Up AWS CloudTrail**

1. **Open the CloudTrail Console**:
   - Navigate to AWS CloudTrail Console.

2. **Create a New Trail**:
   - On the left side-bar, click on **Trails**.
   - Click **Create Trail** to begin the setup process.

3. **Configure the Trail**:
   - **Trail Name**: Give a name to your trail (e.g., `ACC-TY-1113-Trail`).
   - **Storage Location**: Choose the S3 bucket you created earlier (`cloudtrail-logs-bucket`).
   ![TrailNameAndS3](/docs/Lab%202%20CloudTrail/img/TrailNameAndS3.png)

---

### **Step 3: Set Up Encryption and SNS Notifications**

1. **Configure AWS KMS for Encryption**:
   - In the **Customer Managed Key** section, select **New** to create a new AWS KMS key.
   - Give a name to your KMS key (e.g., `ACC-TY-1113-KMS-KEY`).
   ![TrailNew-KMS](/docs/Lab%202%20CloudTrail/img/TrailNew-KMS.png)

2. **Enable SNS Notifications**:
   - In Additional Settings, Tick the option for **SNS Notification Delivery**.
   - Click **Create New SNS Topic** to create a new SNS topic.

3. **Create a New SNS Topic**:
   - Give the SNS topic a name (e.g., `ACC-TY-1113-CloudTrailSNSTopic`).
   - Ensure **CloudWatch Logs** is enabled for better monitoring.
   ![TrailNew-SNSTopic](/docs/Lab%202%20CloudTrail/img/TrailNew-SNSTopic.png)

---

### **Step 4: Set Up IAM Role for CloudTrail**

1. **Create a New IAM Role**:
   - During the trail creation process, you'll be prompted to create a new IAM Role.
   - Give it a name (e.g., `ACC-TY-1113-IAMRole`).
   - Click **Next** to proceed.
   ![TrailNew-SNSTopic](/docs/Lab%202%20CloudTrail/img/TrailNew-CloudWatch.png)

---

### **Step 5: Select Event Types to Log**

1. **Select Management and Data Events**:
   - Enable logging for **Management Events**, **Data Events**, and **Insights Events**.
   ![TrailEventsSelection](/docs/Lab%202%20CloudTrail/img/TrailEventsSelection.png)
   
2. **Select Data Event Types**:
   - Under **Data Event Type**, choose **S3** to monitor bucket activities.
   ![TrailDataEvents-S3](/docs/Lab%202%20CloudTrail/img/TrailDataEvents-S3.png)

3. **Complete the Trail Setup**:
   - Click **Next**, review the settings, and then select **Create Trail**.

---

### **Step 6: Set Up SNS Notifications**

1. **Open the SNS Management Console**:
   - Navigate to AWS SNS Console.

2. **Select the SNS Topic**:
   - In the left side-bar, click on **Topics**.
   - Select the SNS topic you created earlier (e.g., `ACC-TY-1113-CloudTrailSNSTopic`).

3. **Create an Email Subscription**:
   - Click **Create Subscription**.
   - **Protocol**: Select **Email**.
   - **Endpoint**: Enter your email address to receive notifications.
   ![SNS-SubscriptionCreation](/docs/Lab%202%20CloudTrail/img/SNS-SubscriptionCreation.png)

4. **Confirm the Subscription**:
   - Check your email and click the confirmation link to activate the subscription.
   ![SNS-EMailConfirm](/docs/Lab%202%20CloudTrail/img/SNS-EMailConfirm.png)
   ![SNS-SubscriptionConfirmed](/docs/Lab%202%20CloudTrail/img/SNS-SubscriptionConfirmed.png)

---

### **Step 7: Configure CloudWatch Logs for Monitoring**

1. **Open CloudWatch Console**:
   - Navigate to AWS CloudWatch Console.

2. **Select the Log Group**:
   - In the left side-bar, select **Logs**.
   - Find the log group associated with your CloudTrail trail.
   ![CloudWatch-LogGroup](/docs/Lab%202%20CloudTrail/img/CloudWatch-LogGroup.png)

3. **Set Up a CloudWatch Alarm**:
   - Select the Log Group, then Click on **Actions** and then **Anomaly Detection**.
   ![CloudWatch-LogGroup-AnomalySetup](/docs/Lab%202%20CloudTrail/img/CloudWatch-LogGroup-AnomalySetup.png)
   - In **Primary Configuration** select **Evaluation Frequency** as **5 minutes**.
   ![CloudWatch-LogGroup-Anomaly5Min](/docs/Lab%202%20CloudTrail/img/CloudWatch-LogGroup-Anomaly5Min.png)
   - Then Click on **Activate Anomaly Detection**.

---

### **Step 8: Test the Setup**

1. **Upload a File to the S3 Bucket**:
   - Go to your S3 bucket (`acc-ty-1113`) and upload a file.
   ![S3-FileUpload](/docs/Lab%202%20CloudTrail/img/S3-FileUpload.png)

2. **Check CloudWatch Logs**:
   - After uploading the file, you should see new log entries in CloudTrail Event History.
   ![Trail-LogsCheckup](/docs/Lab%202%20CloudTrail/img/Trail-LogsCheckup.png)

3. **Receive SNS Notification**:
   - You will receive an email notification from SNS alerting you about the activity.
   ![SNS-UploadAlertMessage](/docs/Lab%202%20CloudTrail/img/SNS-UploadAlertMessage.png)

---

### **And You're Done!**