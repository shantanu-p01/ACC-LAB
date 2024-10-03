### AWS CloudTrail with CloudWatch and SNS – Detailed Step-by-Step Guide

---

### **Step 1: Create an S3 Bucket for CloudTrail Logs**

1. **Open the S3 Management Console**:
   - Navigate to [AWS S3 Console](https://s3.console.aws.amazon.com/s3/).
   
2. **Create a New Bucket**:
   - Click on **Create Bucket**.
   - Give your bucket a name (e.g., `cloudtrail-logs-bucket`).
   - Choose the region where your bucket will be created.
   
3. **Enable Bucket Versioning**:
   - In the **Bucket Versioning** section, enable versioning. This ensures that multiple versions of logs are retained.
   
4. **Complete Bucket Creation**:
   - Keep all other settings at default, and click **Create Bucket** to finish.

---

### **Step 2: Set Up AWS CloudTrail**

1. **Open the CloudTrail Console**:
   - Navigate to [AWS CloudTrail Console](https://console.aws.amazon.com/cloudtrail/).

2. **Create a New Trail**:
   - On the left menu, click on **Trails**.
   - Click **Create Trail** to begin the setup process.
   
3. **Configure the Trail**:
   - **Trail Name**: Give a meaningful name to your trail (e.g., `CloudTrail-Monitor`).
   - **Storage Location**: Choose the S3 bucket you created earlier (`cloudtrail-logs-bucket`).

---

### **Step 3: Set Up Encryption and SNS Notifications**

1. **Configure AWS KMS for Encryption**:
   - In the **Customer Managed Key** section, select **New** to create a new AWS KMS key.
   - Give a name to your KMS key (e.g., `CloudTrailKMSKey`).

2. **Enable SNS Notifications**:
   - Tick the option for **SNS Notification Delivery**.
   - Click **Create New SNS Topic** to create a new SNS topic.

3. **Create a New SNS Topic**:
   - Give the SNS topic a name (e.g., `CloudTrailNotifications`).
   - Ensure **CloudWatch Logs** is enabled for better monitoring.

---

### **Step 4: Set Up IAM Role for CloudTrail**

1. **Create a New IAM Role**:
   - During the trail creation process, you'll be prompted to create a new IAM Role.
   - Give it a name (e.g., `CloudTrailIAMRole`).
   - Click **Next** to proceed.

---

### **Step 5: Select Event Types to Log**

1. **Select Management and Data Events**:
   - Enable logging for **Management Events**, **Data Events**, and **Insights Events**.
   
2. **Select Data Event Types**:
   - Under **Data Event Type**, choose **S3** to monitor bucket activities.

3. **Complete the Trail Setup**:
   - Click **Next**, review the settings, and then select **Create Trail**.

---

### **Step 6: Set Up SNS Notifications**

1. **Open the SNS Management Console**:
   - Navigate to [AWS SNS Console](https://console.aws.amazon.com/sns/).
   
2. **Select the SNS Topic**:
   - In the left menu, click on **Topics**.
   - Select the SNS topic you created earlier (e.g., `CloudTrailNotifications`).

3. **Create an Email Subscription**:
   - Click **Create Subscription**.
   - **Protocol**: Select **Email**.
   - **Endpoint**: Enter your email address to receive notifications.

4. **Confirm the Subscription**:
   - Check your email and click the confirmation link to activate the subscription.

---

### **Step 7: Configure CloudWatch Logs for Monitoring**

1. **Open CloudWatch Console**:
   - Navigate to [AWS CloudWatch Console](https://console.aws.amazon.com/cloudwatch/).
   
2. **Select the Log Group**:
   - In the left menu, select **Logs**.
   - Find the log group associated with your CloudTrail trail.

3. **Set Up a CloudWatch Alarm**:
   - Click **Actions** and then **Create Alarm**.
   - Select the metric for **Time Anomaly** and set the anomaly detection time to **5 minutes**.

---

### **Step 8: Test the Setup**

1. **Upload a File to the S3 Bucket**:
   - Go to your S3 bucket (`cloudtrail-logs-bucket`) and upload a file.
   
2. **Check CloudWatch Logs**:
   - After uploading the file, you should see new log entries in CloudWatch.

3. **Receive SNS Notification**:
   - You will receive an email notification from SNS alerting you about the activity.

---

### **and you did it!**