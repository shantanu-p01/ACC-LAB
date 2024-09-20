## Lab 4 Auto-Scaling with Load Balancer

### 1. Go to EC2 Service

### 2. Create Security Groups for Application Load Balancer and Auto Scaling Group

#### 2.1. Security Group for Application Load Balancer
- **Name:** Lab4-ApplicationLoadBalancer-Group
- **Inbound Rules:**
  - **Type:** HTTP
  - **Source:** Anywhere-IPV4
- Click **Create Security Group**

#### 2.2. Security Group for Auto Scaling Group
- **Name:** Lab4-AutoScaling-Group
- **Inbound Rules:**
  - **1.** 
    - **Type:** SSH
    - **Source:** Anywhere-IPV4
  - **2.** 
    - **Type:** All TCP
    - **Source:** Lab4-ApplicationLoadBalancer-Group (the security group we just created)
- Click **Create Security Group**

### 3. Create the Auto Scaling Group
- **Enter Name:** Lab4-AutoScaling-Group
- Click **Create** on **Launch Template**
  - **Give Name:** (Choose any)
  - **Select AMI:** (e.g., Ubuntu)
  - **Instance Type:** t2.micro
  - **Create Key Pair:** Save it to your local machine
  - **In Network Settings:** Select the security group we created named **Lab4-AutoScaling-Group**
  - **User Data:** (Mark as Optional)
    ```bash
    #!/bin/bash
    sudo apt update -y && sudo apt upgrade -y && sudo apt install apache2 -y && sudo systemctl start apache2 && sudo systemctl enable apache2 && echo "<h1>This Message is from $(hostname -i)</h1>" > /var/www/html/index.html
    ```
  - Click **Create Launch Template**
- Go back to **Auto Scaling Configuration**, select our **Launch Template**, scroll down, then click on **Next**

### 4. Network Section
- **Select Availability Zones and Subnets:** Select all available zones and subnets
- Click **Next**

### 5. Load Balancing Section
- **Select Load Balancer Type:** Attach to a New Load Balancer
- **Load Balancer Type:** Application Load Balancer
- **Enter Load Balancer Name:** Lab4-ApplicationLoadBalancer
- **Load Balancer Scheme:** Internet-Facing
- **Listeners and Routing:**
  - **Create Target Group:** Port 80 (Automatically created when selecting from the dropdown)
  - **Health Checks:** Check the box to turn on Elastic Load Balancing health checks
- Click **Next**

### 6. Group Size Section
- **Desired Capacity:** 1
- **Minimum Capacity:** 1
- **Maximum Capacity:** 2
- Click **Next** until you reach **Step 7 (Review)**
- Click **Create Auto Scaling Group**

### 7. Modify Load Balancer Security Group
- Go to **Load Balancer**
- **Security Tab:** Verify that it uses the security group of AutoScalingGroup **Lab4-AutoScaling-Group**
- **Change Security Group:**
  - Click on **Edit**
  - Select the Security Group **Lab4-ApplicationLoadBalancer-Group**
  - Click **Save Changes**

### 8. Check EC2 Instances
- **EC2 Instances:** It will show an instance running or being created
- **DNS Name:** Once the Load Balancer is active, copy its DNS name into your browser in a new tab
- You should see a message from your EC2 instance displaying its IP address.

### 9. Dynamic Scaling Policy
- Go to the **Auto Scaling Group Page**, select the **Automatic Scaling** tab, and click on **Create Dynamic Scaling Policy**
- **Policy Type:** Target Tracking Policy
- **Policy Name:** Target Tracking Policy
- **Metric Type:** Average CPU Utilization
- **Target Value:** 30
- Click **Create**

### 10. Check CloudWatch Alarms
- Go to **CloudWatch Service > All Alarms**
- You'll see alarms for scale-in and scale-out operations automatically created by the Auto Scaling Group.

### 11. Test Target Tracking Policy
- **Connect to EC2 Instance:**
  - Go to **EC2 Instance Service** and connect using **EC2 Instance Connect**
  - Run the following commands:
    ```bash
    sudo apt install stress -y
    sudo stress --cpu 12 --timeout 240s
    ```
    *(This command stresses the CPU of the instance for 240 seconds using 12 CPU workers)*
- **Monitor Load:**
  - Go to the **Auto Scaling Group** > **Monitoring** tab > **EC2** sub-tab to see the CPU load graph.
  - The **CloudWatch Alarms** section will show an alarm state once the load is triggered.

### 12. Verify Scaling
- A new EC2 instance will be created automatically. Go to the **Auto Scaling Group** > **Activity** section to see details about the newly created instance.
- Check the **Instance Management** section, where another instance will be shown.
- **Refresh the Browser:** You will see different IP addresses from the new EC2 instances.

### 13. Delete Target Tracking Policy
- In the **Dynamic Scaling Policies** section, delete the **Target Tracking Policy**.

### 14. Create Simple Scaling Policy
- **Go to Dynamic Scaling Policy Section:** Click on **Create Dynamic Scaling Policy**
- **Policy Type:** Simple Scaling
- **Policy Name:** simple-scaling-policy
- **Create CloudWatch Alarm:**
  - **Metric:** CPUUtilization (Select by Auto Scaling Group)
  - **Threshold Type:** Static
  - **Whenever CPUUtilization is Greater than:** 30
  - **Give Alarm Name:** CPUUtilizationAlarm
  - Click **Create Alarm**
- **Go Back to Auto Scaling Configuration:**
  - **Refresh the Alarm Field**
  - Select **CPUUtilizationAlarm**
  - **Take Action:** Add 1
  - Click **Create**

### 15. Set Desired Capacity
- Go to the **Auto Scaling Group > Details Tab > Group Details Section**
- **Lower Desired Capacity to:** 1
- Click **Update**

### 16. Set Alarm State
- **Use AWS CloudShell** to run the following command:
  ```bash
  aws cloudwatch set-alarm-state --alarm-name CPUUtilizationAlarm --state-value ALARM --state-reason "Testing (Lab4)"
  ```

### 17. Verify Alarm
- Go to **CloudWatch Service > Alarms** and check that the alarm is **In Alarm** state.
- A new EC2 instance will be created, as shown in the **Auto Scaling Group > Activity** section.

### 18. Test Load Balancer
- **Verify DNS Name:** The DNS of the Load Balancer will display different IP addresses for the EC2 instances.

### Conclusion
- You've successfully created an Auto Scaling Group and configured scaling policies for both scale-out and scale-in operations.