## Lab 4: Auto-Scaling with Load Balancer

### 1. Go to EC2 Service

### 2. Create Security Groups for Application Load Balancer and Auto Scaling Group

#### 2.1. Security Group for Application Load Balancer
- **Name:** Lab4-ApplicationLoadBalancer-Group-1113
- **Inbound Rules:**
  - **Type:** HTTP
  - **Source:** Anywhere-IPv4
  ![ALB-SG-1113](/docs/Lab%204%20Auto-Scaling%20with%20Load%20Balancer/img/ALB-SG-GROUP-1113.png)
- Click **Create Security Group**

#### 2.2. Security Group for Auto Scaling Group
- **Name:** Lab4-AutoScaling-Group-1113
  ![AS-SG-1113-NAME](/docs/Lab%204%20Auto-Scaling%20with%20Load%20Balancer/img/AS-SG-GROUP-NAME.png)
- **Inbound Rules:**
  - **1.** 
    - **Type:** SSH
    - **Source:** Anywhere-IPv4
    ![AS-SG-1113-1](/docs/Lab%204%20Auto-Scaling%20with%20Load%20Balancer/img/AS-SG-GROUP1-1113.png)
  - **2.** 
    - **Type:** All TCP
    - **Source:** Lab4-ApplicationLoadBalancer-Group-1113 (the security group we just created)
    ![AS-SG-1113-2](/docs/Lab%204%20Auto-Scaling%20with%20Load%20Balancer/img/AS-SG-GROUP2-1113.png)
- Click **Create Security Group**

### 3. Create the Auto Scaling Group
- **Enter Name:** Lab4-AutoScaling-Group-1113
  ![ASG-NAME](/docs/Lab%204%20Auto-Scaling%20with%20Load%20Balancer/img/ASG-Name.png)
- Click **Create** on **Launch Template**
  - **Give Name:** (Choose any)
    ![LaunchTemplateNameDescription](/docs/Lab%204%20Auto-Scaling%20with%20Load%20Balancer/img/LaunchTemplateNameDescription.png)
  - **Select AMI:** Ubuntu
    ![LaunchTemplateAMI](/docs/Lab%204%20Auto-Scaling%20with%20Load%20Balancer/img/LaunchTemplateAMI.png)
  - **Instance Type:** t2.micro
    ![LaunchTemplateInstanceType](/docs/Lab%204%20Auto-Scaling%20with%20Load%20Balancer/img/LaunchTemplateInstanceType.png)
  - **Create Key Pair:** Save it to your local machine
    ![LaunchTemplateKeyPair](/docs/Lab%204%20Auto-Scaling%20with%20Load%20Balancer/img/LaunchTemplateKeyPair.png)
  - **In Network Settings:** Select the security group we created named **Lab4-AutoScaling-Group-1113**
    ![LaunchTemplateNetworkSettings](/docs/Lab%204%20Auto-Scaling%20with%20Load%20Balancer/img/LaunchTemplateNetworkSettings.png)
  - **User Data:** In Additional Settings, scroll down to the bottom and enter the following in the User Data text area field:
    ```bash
    #!/bin/bash
    sudo apt update -y
    sudo apt upgrade -y
    sudo apt install apache2 -y
    sudo systemctl start apache2
    sudo systemctl enable apache2
    echo "<h1>This Message is from $(hostname -i)</h1>" > /var/www/html/index.html
    ```
    ![LaunchTemplateUserData](/docs/Lab%204%20Auto-Scaling%20with%20Load%20Balancer/img/LaunchTemplateUserData.png)
- Click on **Create Launch Template**

### 4. Select Launch Template and Configure Network
- Navigate back to the Auto-Scaling Group creation
- Select the Launch Template we just created
  ![ASG-Template](/docs/Lab%204%20Auto-Scaling%20with%20Load%20Balancer/img/ASG-Template.png)
- Click **Next**
- **Network Section:**
  - **Select Availability Zones and Subnets:** Select all available zones and subnets
    ![ASG-NetworkSection](/docs/Lab%204%20Auto-Scaling%20with%20Load%20Balancer/img/ASG-NetworkSection.png)
- Click **Next**

### 5. Configure Load Balancing
- **Select Load Balancer Type:** Attach to a New Load Balancer
  ![ASG-LoadBalancerSelection](/docs/Lab%204%20Auto-Scaling%20with%20Load%20Balancer/img/ASG-LoadBalancerSelection.png)
- **Load Balancer Type:** Application Load Balancer
- **Enter Load Balancer Name:** Lab4-ALB-1113
- **Load Balancer Scheme:** Internet-Facing
  ![ASG-LoadBalancer-TypeNameScheme](/docs/Lab%204%20Auto-Scaling%20with%20Load%20Balancer/img/ASG-LoadBalancer-TypeNameScheme.png)
- **Listeners and Routing:**
  - **Create Target Group:** Port 80 (Automatically created when selecting from the dropdown)
  ![ASG-LoadBalancerListenersAndRouting](/docs/Lab%204%20Auto-Scaling%20with%20Load%20Balancer/img/ASG-LoadBalancerListenersAndRouting.png)
- **Health Checks:** Check the box to turn on Elastic Load Balancing health checks
  ![ASG-LoadBalancerHealthChecks](/docs/Lab%204%20Auto-Scaling%20with%20Load%20Balancer/img/ASG-LoadBalancerHealthChecks.png)
- Click **Next**

### 6. Configure Group Size
- **Desired Capacity:** 1
  ![ASG-GroupSizeDesiredCapacity](/docs/Lab%204%20Auto-Scaling%20with%20Load%20Balancer/img/ASG-GroupSizeDesiredCapacity.png)
- **Minimum Capacity:** 1
- **Maximum Capacity:** 2
  ![ASG-GroupSizeMinMaxCapacity](/docs/Lab%204%20Auto-Scaling%20with%20Load%20Balancer/img/ASG-GroupSizeMinMaxCapacity.png)
- Click **Next** until you reach **Step 7 (Review)**
- Click **Create Auto Scaling Group**

### 7. Modify Load Balancer Security Group
- Go to **Load Balancer**
- **Security Tab:** Verify that it uses the security group of AutoScalingGroup **Lab4-AutoScaling-Group-1113**
- **Change Security Group:**
  - Click on **Edit**
  - Select the Security Group **Lab4-ApplicationLoadBalancer-Group-1113**
  ![LB-SG-Selection](/docs/Lab%204%20Auto-Scaling%20with%20Load%20Balancer/img/LB-SG-Selection.png)
  - Click **Save Changes**

### 8. Check EC2 Instances
- **EC2 Instances:** It will show an instance running or being created
  ![EC2-CheckInstances](/docs/Lab%204%20Auto-Scaling%20with%20Load%20Balancer/img/EC2-CheckInstances.png)
- **DNS Name:** Once the Load Balancer is active, copy its DNS name into your browser in a new tab
  ![LB-DNS-Check](/docs/Lab%204%20Auto-Scaling%20with%20Load%20Balancer/img/LB-DNS-Check.png)
- You should see a message from your EC2 instance displaying its IP address.
  ![LB-URL-Worked](/docs/Lab%204%20Auto-Scaling%20with%20Load%20Balancer/img/LB-URL-Worked.png)
NOTE: Don't forget to remove HTTPS from the URL.

### 9. Create Dynamic Scaling Policy
- Go to the **Auto Scaling Group** we have created, select the **Automatic Scaling** tab, and click on **Create Dynamic Scaling Policy**
  ![AS-CreateDynamicPolicy](/docs/Lab%204%20Auto-Scaling%20with%20Load%20Balancer/img/AS-CreateDynamicPolicy.png)
- **Policy Type:** Target Tracking Policy
- **Policy Name:** Target Tracking Policy
- **Metric Type:** Average CPU Utilization
- **Target Value:** 30
  ![ASG-DynamicPolicyConfig](/docs/Lab%204%20Auto-Scaling%20with%20Load%20Balancer/img/ASG-DynamicPolicyConfig.png)
- Click **Create**

### 10. Check CloudWatch Alarms
- Go to **CloudWatch Service > All Alarms**
- You'll see alarms for scale-in and scale-out operations automatically created by the Auto Scaling Group.
  ![CloudWatch-AllAlarmsCheck](/docs/Lab%204%20Auto-Scaling%20with%20Load%20Balancer/img/CloudWatch-AllAlarmsCheck.png)

### 11. Test Target Tracking Policy
- **Connect to EC2 Instance:**
  - Go to **EC2 Instance Service** and connect using **EC2 Instance Connect**
  - Run the following commands:
    ```bash
    sudo apt install stress -y
    sudo stress --cpu 12 --timeout 240s
    ```

### 12. Verify Scaling
- A new EC2 instance will be created automatically. Go to the **Auto Scaling Group > Activity** section to see details about the newly created instance.
  ![ASG-ActivityHistoryCheckNewEC2](/docs/Lab%204%20Auto-Scaling%20with%20Load%20Balancer/img/ASG-ActivityHistoryCheckNewEC2.png)
  ![EC2-NewEc2ByASG](/docs/Lab%204%20Auto-Scaling%20with%20Load%20Balancer/img/EC2-NewEc2ByASG.png)
- Check the **Instance Management** section, where another instance will be shown.
- **Refresh the Browser:** You will see different IP addresses from the new EC2 instances.
  ![LB-URL-Worked](/docs/Lab%204%20Auto-Scaling%20with%20Load%20Balancer/img/LB-URL-NewInstance.png)
  ![LB-URL-NewInstance](/docs/Lab%204%20Auto-Scaling%20with%20Load%20Balancer/img/LB-URL-NewInstance.png)

### 13. Delete Target Tracking Policy
- Navigate back to the **Auto Scaling Group** we have created, select the **Automatic Scaling** Tab
- Select all the **Dynamic scaling policies**, click on **Actions**, then click on **Delete**
  ![ASG-DeletingDynamicScalingPolicies](/docs/Lab%204%20Auto-Scaling%20with%20Load%20Balancer/img/ASG-DeletingDynamicScalingPolicies.png)

### 14. Create Simple Scaling Policy
- **Go to Dynamic Scaling Policy Section:** Click on **Create Dynamic Scaling Policy**
- **Policy Type:** Simple Scaling
- **Policy Name:** simple-scaling-policy
- **Create CloudWatch Alarm:**
  - **Metric:** EC2 > Select by Auto Scaling Group > CPUUtilization
  ![NewCloudWatch-EC2Metric](/docs/Lab%204%20Auto-Scaling%20with%20Load%20Balancer/img/NewCloudWatch-EC2Metric.png)
  ![NewCloudWatch-ByASG](/docs/Lab%204%20Auto-Scaling%20with%20Load%20Balancer/img/NewCloudWatch-ByASG.png)
  ![NewCloudWatch-CPU-Utilization](/docs/Lab%204%20Auto-Scaling%20with%20Load%20Balancer/img/NewCloudWatch-CPU-Utilization.png)
  - **Threshold Type:** Static
  - **Whenever CPUUtilization is Greater than:** 30
  - **Give Alarm Name:** CPUUtilizationAlarm
  ![NewCloudWatch-RestConfig](/docs/Lab%204%20Auto-Scaling%20with%20Load%20Balancer/img/NewCloudWatch-RestConfig.png)
  - Click **Next**
- Select **Alarm State Trigger**: InAlarm
- **Send a notification to the following SNS topic**: Create New Topic
- **Email endpoints that will receive the notification…**: (Enter Your Email)
  ![NewCloudWatch-SNS-Topic](/docs/Lab%204%20Auto-Scaling%20with%20Load%20Balancer/img/NewCloudWatch-SNS-Topic.png)
- Then click on **Create Topic**
  ![NewCloudWatch-SNS-Topic-Created](/docs/Lab%204%20Auto-Scaling%20with%20Load%20Balancer/img/NewCloudWatch-SNS-Topic-Created.png)
- Then click **Next** and **Enter Alarm Name** e.g.,
  ![NewCloudWatch-AlarmName](/docs/Lab%204%20Auto-Scaling%20with%20Load%20Balancer/img/NewCloudWatch-AlarmName.png)
- Then click **Next**, review all the Configurations, and click on **Create Alarm**
- Navigate back to the **Auto Scaling Group** Page's **Create Dynamic Scaling Policy** Section and select the **CloudWatch alarm** we just created
  ![ASG-SimpleScalingAlarmSelection](/docs/Lab%204%20Auto-Scaling%20with%20Load%20Balancer/img/ASG-SimpleScalingAlarmSelection.png)
- In **Take the action** field update the value to **1**
- Then click on **Create**

### 15. Set Desired Capacity
- Go back to the **Auto Scaling Group > Details Tab > Group Details Section**
- **Lower Desired Capacity to:** 1
  ![ASG-Details-DesiredCapacitySetTo1](/docs/Lab%204%20Auto-Scaling%20with%20Load%20Balancer/img/ASG-Details-DesiredCapacitySetTo1.png)
- Click **Update**

### 16. Set Alarm State
- **Use AWS CloudShell** to run the following command:
  ![AWS-CloudShell](/docs/Lab%204%20Auto-Scaling%20with%20Load%20Balancer/img/AWS-CloudShell.png)
  ```bash
  aws cloudwatch set-alarm-state --alarm-name <Your Alarm Name Goes Here> --state-value ALARM --state-reason "Testing (Lab4)"
  ```
  ![AWS-CloudShell-Command](/docs/Lab%204%20Auto-Scaling%20with%20Load%20Balancer/img/AWS-CloudShell-Command.png)

### 17. Verify Alarm
- Go to **CloudWatch Service > Alarms** and check that the alarm is in the **In Alarm** state.
  ![NewCloudWatch-InAlarmState](/docs/Lab%204%20Auto-Scaling%20with%20Load%20Balancer/img/NewCloudWatch-InAlarmState.png)
- A new EC2 instance will be created, as shown in the **Auto Scaling Group > Activity** section.
  ![NewCloudWatchAlarm-NewEC2-Launched](/docs/Lab%204%20Auto-Scaling%20with%20Load%20Balancer/img/NewCloudWatchAlarm-NewEC2-Launched.png)

### 18. Test Load Balancer
- **Verify DNS Name:** The DNS of the Load Balancer will display different IP addresses for the EC2 instances.
  ![EC2-SimpleScaling1URL](/docs/Lab%204%20Auto-Scaling%20with%20Load%20Balancer/img/EC2-SimpleScaling1URL.png)
  ![EC2-SimpleScaling2URL](/docs/Lab%204%20Auto-Scaling%20with%20Load%20Balancer/img/EC2-SimpleScaling2URL.png)

### Conclusion
You've successfully created an Auto Scaling Group and configured scaling policies for both scale-out and scale-in operations.