## Lab 5: Setting Up an RDS Instance, Connecting with MySQL Workbench, and Inserting Data into a Table

### Step 1: Create a Database in RDS

1. **Go to the RDS Service**  
   - In your AWS Management Console, search for and go to the **RDS** service.

2. **Click on Create Database**  
   - Click on the **Create database** button.

3. **Choose a Database Creation Method**  
   - Select **Standard create** in the 'Choose a database creation method' section.  
     ![Standard Create](/docs/Lab%205%20RDS%20Setup%20And%20Data%20Insertion/img/databaseCreationMethod.png)

4. **Select Engine Type**  
   - In the 'Engine Options' section, choose **MySQL**.  
     ![Engine Type](/docs/Lab%205%20RDS%20Setup%20And%20Data%20Insertion/img/engineTypes.png)

5. **Select Free Tier Template**  
   - In the 'Templates' section, select **Free Tier**.  
     ![Templates](/docs/Lab%205%20RDS%20Setup%20And%20Data%20Insertion/img/templateFreeTier.png)

6. **Enter DB Instance Identifier and Credentials**  
   - In the 'Settings' section, enter the **DB instance identifier** (name for your RDS instance) and the **credentials** (username and password) for the root user.  
     ![Name, Credentials](/docs/Lab%205%20RDS%20Setup%20And%20Data%20Insertion/img/settingsSectionNameUsernamePassword.png)

7. **Configure Connectivity**  
   - In the 'Connectivity' section, select **Public Access** as **Yes**, and choose the **default VPC**.  
     ![Public Access, VPC](/docs/Lab%205%20RDS%20Setup%20And%20Data%20Insertion/img/connectivityPublicAccessVPC.png)

8. **Create the Database**  
   - Scroll down and click on **Create Database**.  
   - Wait for the database to be created successfully.

### Step 2: Create a Security Group

1. **Search for Security Groups**  
   - After creating the database, search for **Security Groups** in the AWS Management Console.  
     ![SG-Search](/docs/Lab%205%20RDS%20Setup%20And%20Data%20Insertion/img/sgSearch.png)

2. **Create a Security Group**  
   - Click on the **Create Security Group** button.  
   
3. **Enter Basic Details**  
   - In the 'Basic Details' section, enter the **Security Group Name** and **Description**.  
     ![SG-Name, SG-Description](/docs/Lab%205%20RDS%20Setup%20And%20Data%20Insertion/img/basicDetailsSG.png)

4. **Add Inbound Rule**  
   - In the 'Inbound Rule' section, click on **Add Rule**.  
   - Select **Type** as **MYSQL/AURORA** and **Source** as **Anywhere IPv4** from their respective dropdowns.  
     ![Inbound Rule](/docs/Lab%205%20RDS%20Setup%20And%20Data%20Insertion/img/iboundRule-sg.png)

5. **Create the Security Group**  
   - Click on **Create Security Group**.

### Step 3: Modify RDS to Use the Security Group

1. **Select Your Database**  
   - Go back to the **database** you just created.  
   - Select the database and click on the **Modify** button.  
     ![dbModifyBtn](/docs/Lab%205%20RDS%20Setup%20And%20Data%20Insertion/img/dbModifyBtn.png)

2. **Select Security Group**  
   - Scroll down to the 'Connectivity' section and in the **Security Group** field, select the **Security Group** you just created.  
     ![RDS Modification Confirmation](/docs/Lab%205%20RDS%20Setup%20And%20Data%20Insertion/img/rdsSGSelection.png)

3. **Apply Changes**  
   - Click on **Continue**, then in the 'Schedule Modifications' section, select **Apply Immediately** and click on **Modify DB Instance**.  
     ![RDS Modification Confirmation](/docs/Lab%205%20RDS%20Setup%20And%20Data%20Insertion/img/rdsModfiyConfirmation.png)

### Step 4: Install and Configure MySQL Workbench

1. **Download MySQL Workbench**  
   - Go to the [MySQL Workbench Website](https://dev.mysql.com/downloads/workbench/) and download the MySQL Workbench.  
   - Install it by following the [guided setup](https://hitohitonomis-my.sharepoint.com/:v:/g/personal/gawd_hitohitonomi_cloud/Eb8IisLRTfNMuSjR5Q9lXj4BOo_wtRlnyFwxQSRnbfExIg?e=ovVbNq&nav=eyJyZWZlcnJhbEluZm8iOnsicmVmZXJyYWxBcHAiOiJTdHJlYW1XZWJBcHAiLCJyZWZlcnJhbFZpZXciOiJTaGFyZURpYWxvZy1MaW5rIiwicmVmZXJyYWxBcHBQbGF0Zm9ybSI6IldlYiIsInJlZmVycmFsTW9kZSI6InZpZXcifX0%3D).

2. **Open MySQL Workbench**  
   - After installing, open the **MySQL Workbench**.

3. **Create a New MySQL Connection**  
   - In the 'My Connections' section, click the **+** icon to create a new connection.  
     ![MySQL Connection Setup](/docs/Lab%205%20RDS%20Setup%20And%20Data%20Insertion/img/mysqlConnectionSetup.png)

4. **Enter Hostname and Credentials**  
   - Go back to your **RDS instance** in the AWS Console, and copy the **endpoint** from the 'Connectivity & Security' tab.  
     ![RDS Endpoint](/docs/Lab%205%20RDS%20Setup%20And%20Data%20Insertion/img/rdsEndpoint.png)  
   - In MySQL Workbench, paste this endpoint into the **Hostname** field.  
   - Enter a **Connection Name**, **Master/Root Username**, and click **Store in Vault** to enter your password.
     ![Test Connection](/docs/Lab%205%20RDS%20Setup%20And%20Data%20Insertion/img/testRDSConnection.png)
5. **Test Connection**  
   - Click on the **Test Connection** button. If successful, you will see a message like:  
     ![Connection Success](/docs/Lab%205%20RDS%20Setup%20And%20Data%20Insertion/img/RDS-MySQL-ConnectionSuccess.png)  
   - Click **OK** to close the popup, and then click **OK** again to create the connection.  
     ![Create Connection](/docs/Lab%205%20RDS%20Setup%20And%20Data%20Insertion/img/createConnection.png)

6. **Open the Connection**  
   - Click on the new connection to open it.  
     ![Connection Created](/docs/Lab%205%20RDS%20Setup%20And%20Data%20Insertion/img/connectionCreated.png)

### Step 5: Create Database and Table in MySQL Workbench

1. **Create Database and Table**  
   - In the **Query 1** tab, enter the following SQL commands:

        ```sql
        CREATE DATABASE student;
        USE student;
        CREATE TABLE students (
            id INT PRIMARY KEY AUTO_INCREMENT,
            name VARCHAR(255) NOT NULL,
            number VARCHAR(20),
            email VARCHAR(255) UNIQUE NOT NULL
        );
        ```

   - Click the **Yellow lightning button** to execute the code. You should see a success message.  
     ![DB, Table Creation](/docs/Lab%205%20RDS%20Setup%20And%20Data%20Insertion/img/databaseTableCreation.png)

### Step 6: Insert Data into Table

1. **Insert Data**  
   - Remove the previous command and enter the following SQL command to insert data into the table:

        ```sql
        INSERT INTO students (name, number, email)
        VALUES 
        ('Shantanu', '1234567890', 'shantanu@example.com'),
        ('Shiv', '2345678901', 'shiv@example.com'),
        ('Raju', '3456789012', 'raju@example.com'),
        ('Om', '4567890123', 'om@example.com'),
        ('Smit', '5678901234', 'smit@example.com');
        ```

   - Hit the **execute** button, and the output will show success.  
     ![Inserting Data into Table](/docs/Lab%205%20RDS%20Setup%20And%20Data%20Insertion/img/dataInsertionIntoTable.png)

### Step 7: View Data from the Table

1. **View Data**  
   - Remove the old commands, and enter the following SQL command to view the data:

        ```sql
        SELECT * FROM students;
        ```

   - Execute the command, and you will see the data displayed.  
     ![Table Data Displayed](/docs/Lab%205%20RDS%20Setup%20And%20Data%20Insertion/img/dataDisplay.png)

### Conclusion:
You have successfully created an RDS instance, connected it using MySQL Workbench, created a database and table, inserted data, and displayed it.