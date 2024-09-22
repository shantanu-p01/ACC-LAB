## Lab 1: CloudWatch + Lambda + SNS

**Configuring CloudWatch Alarm for Lambda Invocation Errors with SNS Notifications**

This guide walks you through setting up a **CloudWatch Alarm** to monitor AWS Lambda errors and notify you via **SNS (Simple Notification Service)** when the threshold is exceeded. Notifications will be sent to an email address of your choice.

---

### Step 1: Create a Lambda Function

1. Go to the **Lambda Service** in the AWS Management Console.
2. Click **Create Function**.
3. Select **Author from Scratch**.
4. Enter a **function name**.
5. Set the **runtime** to **Node.js 20**.
6. Click **Create Function** to finish.

![Lambda Function Creation](/docs/Lab%201%20CloudWatch%20+%20SNS/img/lambdaFunctionCreation.png)

---

### Step 2: Monitor Lambda Metrics

1. After the function is created, navigate to your Lambda function.
2. Select the **Monitor** tab, then click on the **Metrics** sub-tab.
3. You will see metrics like **Error Count** and **Success Rate (%)**.

These metrics will allow us to set up an alarm that triggers when the error count exceeds a certain threshold.

![Lambda Function Monitor Error Count](/docs/Lab%201%20CloudWatch%20+%20SNS/img/lambdaFunctionMonitorErrorCount.png)

---

### Step 3: Create an SNS Topic for Notifications

1. Navigate to the **Simple Notification Service (SNS)** in the AWS console.
2. In the left panel, click **Topics**.
3. Click **Create Topic**.
4. Select **Standard** as the type of the topic.
5. Enter a **name** for the topic.
6. Click **Create Topic**.

![SNS Topic Creation](/docs/Lab%201%20CloudWatch%20+%20SNS/img/SNSTopicCreation.png)

---

### Step 4: Subscribe to the SNS Topic

1. After the topic is created, go to the **Subscriptions** tab for that topic.
2. Click **Create Subscription**.
3. In the **Create Subscription** section:
   - Select **Email** as the protocol.
   - Enter your **email address** where you want to receive notifications.
4. Click **Create Subscription**.

![SNS Topic Subscription Creation](/docs/Lab%201%20CloudWatch%20+%20SNS/img/SNSTopicSubscriptionCreation.png)

5. The status of the subscription will be **Pending**. Go to your email and confirm the subscription.

![SNS Topic Subscription Pending](/docs/Lab%201%20CloudWatch%20+%20SNS/img/SNSTopicSubscriptionPending.png)

6. After confirmation, the status will change to **Confirmed**.

![SNS Topic Subscription Success](/docs/Lab%201%20CloudWatch%20+%20SNS/img/SNSTopicSubscriptionSuccess.png)

---

### Step 5: Test the Lambda Function

1. Return to your Lambda function, and go to the **Code** tab.
2. Click the dropdown next to the **Test** button, then select **Configure Test Event**.

![Lambda Function Event Configuration Dropdown](/docs/Lab%201%20CloudWatch%20+%20SNS/img/lambdaFunctionEventConfigurationDropdown.png)

3. Enter an **event name**.
4. Click **Save**.

![Lambda Function Event Configuration Details](/docs/Lab%201%20CloudWatch%20+%20SNS/img/lambdaFunctionEventConfigurationDetails.png)

5. Now, click **Test** to execute your Lambda function.

**Note**: The error metrics may take some time to reflect in the **Monitor** tab.

---

### Step 6: Create a CloudWatch Alarm

1. Go to the **CloudWatch** service in the AWS console.
2. Click **Create Alarm**.
3. Click **Select Metrics**.
4. In the **Metrics** section, select **Lambda Metrics**.
5. Choose the **By Function Name** option.
6. Select your Lambda function, and choose the **Errors** metric.
7. Click **Select Metric**.
8. In the **Specify Metric and Conditions** section:
   - In the **Statistics** field, change the default **Average** to **Maximum**.

   ![CloudWatch Metric Statistics](/docs/Lab%201%20CloudWatch%20+%20SNS/img/cloudWatchMetricStats.png)

   - In the **Conditions** section, set the threshold type to **Static**.
   - Under **Whenever Error Count is**, select **Greater Than or Equal to**.
   - Set the value to `1`.

   ![CloudWatch Metric Conditions](/docs/Lab%201%20CloudWatch%20+%20SNS/img/cloudWatchMetricConditions.png)

9. Click **Next**.

---

### Step 7: Set Up Notifications for the Alarm

1. In the **Notifications** section, set the **Alarm State Trigger** to **In Alarm**.
2. Under **Send a Notification to**, select **Existing SNS Topic**.
3. Choose the SNS topic you created earlier.
4. The email endpoint you provided will appear in the notification settings.
5. Click **Next**.

![CloudWatch Metric Notifications](/docs/Lab%201%20CloudWatch%20+%20SNS/img/cloudWatchMetricNotifications.png)

---

### Step 8: Name and Create the Alarm

1. Enter a name for your alarm.
2. Click **Next**, then **Create Alarm**.

![CloudWatch Alarm Creation](/docs/Lab%201%20CloudWatch%20+%20SNS/img/cloudWatchAlarmInsufficientData.png)

---

### Step 9: Trigger the Alarm with a Lambda Error

1. Go back to your Lambda function.
2. Introduce an intentional error in the code (for example, change `JSON` to `JON`).
3. Click **Deploy** to save your changes.
4. Click **Test** 4 to 5 times to invoke the function and produce errors.

---

### Step 10: Verify the CloudWatch Alarm

1. Go back to the **CloudWatch** service.
2. Check the state of your alarm, which will be set to **In Alarm** if errors were detected.

![CloudWatch Alarm In Alarm](/docs/Lab%201%20CloudWatch%20+%20SNS/img/cloudWatchAlarmInAlarm.png)

**Note**: If the alarm state does not change immediately, wait a few minutes, as it may take time to reflect the new state.

---

### Step 11: Receive SNS Email Notification

Once the alarm state changes to **In Alarm**, you should receive an email notification at the email address you provided during the SNS subscription setup.

![SNS Email Received](/docs/Lab%201%20CloudWatch%20+%20SNS/img/emailReceived.png)

---

### Conclusion

By following these steps, you have successfully configured a CloudWatch Alarm for Lambda errors and set up SNS to notify you via email when the alarm is triggered.