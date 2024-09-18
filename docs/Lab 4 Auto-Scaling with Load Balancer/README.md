### Lab 4: Auto-Scaling with Load Balancer

This lab walks through the steps of setting up Auto Scaling with an Application Load Balancer (ALB) on AWS, configuring security groups, launching EC2 instances, and implementing scaling policies for dynamic resource management.

---

### Step 1: Create Security Groups for ALB and Auto Scaling Group

#### 1.1 Security Group for Application Load Balancer
1. Go to the **EC2** service in your AWS Management Console.
2. Select **Security Groups** from the left-hand menu and click **Create Security Group**.
   - **Security Group Name**: `Lab4-ApplicationLoadBalancer-Group`
   - **Inbound Rule**:
     - **Type**: HTTP
     - **Source**: Anywhere (0.0.0.0/0)
3. Click **Create Security Group**.

#### 1.2 Security Group for Auto Scaling Group
1. Go back to **Security Groups** and create another security group.
   - **Security Group Name**: `Lab4-AutoScaling-Group`
   - **Inbound Rules**:
     1. **Type**: SSH
        - **Source**: Anywhere (0.0.0.0/0)
     2. **Type**: All TCP
        - **Source**: Select the `Lab4-ApplicationLoadBalancer-Group` as the source.
2. Click **Create Security Group**.

---

### Step 2: Create the Auto Scaling Group

#### 2.1 Create Launch Template
1. In the **Auto Scaling Groups** section, click **Create Auto Scaling Group**.
2. Enter the **Auto Scaling Group Name**: `Lab4-AutoScaling-Group`.
3. Click on **Create Launch Template**.
   - **Template Name**: Give your template a name (e.g., `Lab4-LaunchTemplate`).
   - **AMI**: Choose your AMI (e.g., Ubuntu).
   - **Instance Type**: Select `t2.micro`.
   - **Key Pair**: Create a key pair and save it to your local machine.
   - **Network Settings**: Select the security group `Lab4-AutoScaling-Group`.
   - **User Data**: Enter the following script in the User Data field:
     ```bash
     #!/bin/bash
     sudo apt update -y && sudo apt upgrade -y && sudo apt install httpd -y
     sudo systemctl start httpd && sudo systemctl enable httpd
     echo "<h1>This message is from $(hostname -i)</h1>" > /var/www/html/index.html
     ```
4. Click **Create Launch Template**.

#### 2.2 Complete Auto Scaling Group Configuration
1. Go back to the **Auto Scaling Group** creation page, select the **Launch Template** you just created.
2. In the **Network** section, select the available **Availability Zones** and **Subnets**.
3. Click **Next**.
4. In the **Load Balancing** section:
   - Select **Attach to a New Load Balancer**.
   - Choose **Application Load Balancer**.
   - **Load Balancer Name**: `Lab4-ApplicationLoadBalancer`.
   - **Scheme**: Internet-facing.
   - **Listeners and Routing**: Create a new target group on port 80.
   - Check **Turn on Elastic Load Balancing Health Checks**.
5. Click **Next**.

#### 2.3 Configure Group Size
1. In the **Group Size** section, set the following:
   - **Desired Capacity**: 1
   - **Minimum Capacity**: 1
   - **Maximum Capacity**: 2
2. Click **Next** and continue through the remaining steps until you reach the **Review** section. 
3. Click **Create Auto Scaling Group**.

---

### Step 3: Configure Load Balancer

1. Go to the **Load Balancer** section in EC2.
2. Once the **Load Balancer** is created, select it and navigate to the **Security** tab.
3. Edit the security group and replace it with `Lab4-ApplicationLoadBalancer-Group`.
4. Click **Save Changes**.

---

### Step 4: Verify EC2 Instance

1. Go to the **EC2 Instances** section. You will see an instance running or being created.
2. Once the **Load Balancer** is active, copy its **DNS Name** and open it in a browser.
3. The webpage should display a message with the IP address of your EC2 instance.
   
---

### Step 5: Create a Dynamic Scaling Policy

1. Go to the **Auto Scaling Group** and navigate to the **Automatic Scaling** tab.
2. Click **Create Dynamic Scaling Policy**.
   - **Policy Type**: Target Tracking Policy.
   - **Policy Name**: `Target Tracking Policy`.
   - **Metric Type**: Average CPU Utilization.
   - **Target Value**: 30%.
3. Click **Create**.

#### 5.1 CloudWatch Alarms
- A CloudWatch alarm is automatically created for scaling in and scaling out operations. You can verify this by going to the **CloudWatch** service and checking the **Alarms** section.

---

### Step 6: Test Dynamic Scaling Policy

1. Go to **EC2 Instances** and connect to the running instance using **EC2 Instance Connect**.
2. Install the stress package by running:
   ```bash
   sudo apt install stress -y
   ```
3. To put load on the instance, run the following command:
   ```bash
   sudo stress --cpu 12 --timeout 240s
   ```
   This command generates CPU load for 240 seconds using 12 virtual cores.
4. Go back to the **Auto Scaling Group** and under the **Monitoring** tab, you will see the load on the EC2 instance. CloudWatch alarms will trigger, and a new instance will be created automatically.
5. Once a new instance is created, refresh the webpage (DNS of the Load Balancer). You should see messages from different IP addresses (representing different EC2 instances).

---

### Step 7: Delete Target Tracking Policy

1. Go to **Auto Scaling Group** > **Dynamic Scaling Policies**.
2. Delete the `Target Tracking Policy` by selecting it and clicking **Actions > Delete**.

---

### Step 8: Create Simple Scaling Policy

1. Go to the **Dynamic Scaling Policies** section and click **Create Dynamic Scaling Policy**.
2. Select **Simple Scaling Policy**.
   - **Policy Name**: `simple-scaling-policy`.
3. Click **Create CloudWatch Alarm** and select the following:
   - **Metric**: CPU Utilization (from Auto Scaling group).
   - **Statistics**: Average.
   - **Threshold Type**: Static.
   - **Condition**: Greater than 30%.
4. Remove notifications and name the alarm `CPUUtilizationAlarm`.
5. Go back to **Auto Scaling Group** and select the **CPUUtilizationAlarm** for the new policy.
6. Set the action to add **1 instance** and click **Create**.

#### 8.1 Trigger Alarm
1. Lower the **Desired Capacity** to 1 in the Auto Scaling group.
2. Trigger the alarm using AWS CloudShell:
   ```bash
   aws cloudwatch set-alarm-state --alarm-name CPUUtilizationAlarm --state-value ALARM --state-reason "Testing (Lab4)"
   ```
3. The alarm will go into the **In Alarm** state, triggering the creation of a new EC2 instance.

---

### Conclusion
You have successfully created an Auto Scaling Group with Load Balancer, configured scaling policies, and tested them by generating CPU load. The setup dynamically adjusts the number of EC2 instances based on system load.

