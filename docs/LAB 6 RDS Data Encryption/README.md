### Step-by-Step Guide to Encrypt an Unencrypted RDS Database
---
#### 1. Go to AWS Console and Search for RDS
- Navigate to the RDS section in the AWS Management Console.

![RDS Main Page](/docs/LAB%206%20RDS%20Data%20Encryption/img/rdsMainPage.png)


#### 2. Create a New Database
- Click on **Create Database**.

![RDS Create Database](/docs/LAB%206%20RDS%20Data%20Encryption/img/chooseADatabaseCreationMethod.png)


#### 3. Select Database Creation Method
- Under **Choose a Database Creation Method**, select **Standard Create**.

![RDS Choose A Database Creation Method](/docs/LAB%206%20RDS%20Data%20Encryption/img/chooseADatabaseCreationMethod.png)


#### 4. Choose Engine Options
- In the **Engine Options** section, choose **MySQL** as the database engine.

![RDS Engine Options](/docs/LAB%206%20RDS%20Data%20Encryption/img/engineOptionsMYSQL.png)


#### 5. Select Free Tier Template
- In the **Templates** section, select **Free Tier**.

![RDS Template Free Tier](/docs/LAB%206%20RDS%20Data%20Encryption/img/tempalteSectionFreeTier.png)


#### 6. Set Database Instance Identifier
- In the **Settings** section, enter the **DB Instance Identifier** name.

![RDS DB Identifier Name](/docs/LAB%206%20RDS%20Data%20Encryption/img/settingsDBIdentifierName.png)


#### 7. Set Username and Password
- In the **Credentials** section, enter your **Username**, **Password**, and **Confirm Password**.

![RDS Credentials](/docs/LAB%206%20RDS%20Data%20Encryption/img/credentialsUsernamePassword.png)


#### 8. Enable Public Access
- In the **Connectivity** section, enable **Public Access** by selecting the **Yes** radio button.

![RDS Public Access](/docs/LAB%206%20RDS%20Data%20Encryption/img/connectivityPublicAccess.png)


#### 9. Disable Encryption
- Scroll down to the **Additional Configuration** section. In the **Encryption** field, uncheck the box to disable encryption.

![RDS Disable Encryption](/docs/LAB%206%20RDS%20Data%20Encryption/img/additionalConfigurationDisableEncryption.png)


#### 10. Create Database
- Click on **Create Database** and wait a few minutes for the database to be successfully created.

![RDS Create Success](/docs/LAB%206%20RDS%20Data%20Encryption/img/rdsCreatedSuccessfully.png)


#### 11. Take a Snapshot of the Unencrypted Database
- After the database is created, click on the **Actions** button, and select **Take Snapshot**.

![RDS Take Snapshot](/docs/LAB%206%20RDS%20Data%20Encryption/img/actionsTakeSnapshots.png)

- Enter a name for the snapshot.

![RDS Snapshot Name](/docs/LAB%206%20RDS%20Data%20Encryption/img/snapshotPreferencesName.png)

- Click on **Create Snapshot** and wait for the snapshot to be created.

![RDS Snapshot Getting Created](/docs/LAB%206%20RDS%20Data%20Encryption/img/snapshotGettingCreated.png)


#### 12. Copy Snapshot and Enable Encryption
- Once the snapshot is created, refresh the page.
- Select the snapshot, click on the **Actions** button, and choose **Copy Snapshot**.

![RDS Copy Snapshot](/docs/LAB%206%20RDS%20Data%20Encryption/img/snapshotCopySnapshot.png)

- In the **New DB Snapshot Identifier** field, enter a name for the snapshot and choose the **Destination Region**.

![RDS Copied Snapshot DB Identifer and Destination Region](/docs/LAB%206%20RDS%20Data%20Encryption/img/settingsNewDBSnapshotIdentifier.png)

- Scroll down to the **Encryption** field and check the box to **Encrypt the Snapshot**.

![RDS Enable Encryption](/docs/LAB%206%20RDS%20Data%20Encryption/img/enableEncryption.png)

- Click on **Copy Snapshot** and wait for the snapshot to be copied and encrypted.

![RDS Encrypted Snapshot Getting Created](/docs/LAB%206%20RDS%20Data%20Encryption/img/snapshotGettingCopied.png)


#### 13. Restore the Encrypted Snapshot
- Once the encrypted snapshot is created, select it, click on the **Actions** button, and choose **Restore Snapshot**.

![RDS Restore Encrypted Snapshot](/docs/LAB%206%20RDS%20Data%20Encryption/img/restoreEncryptedSnapshot.png)

- In the **Availability and Durability** section, choose the **Single DB Instance** option.

![RDS Encrypted Snapshot Availability and Durability](/docs/LAB%206%20RDS%20Data%20Encryption/img/encryptedSnapshotAvailalbilityAndDurability.png)

- In the **Settings** section, enter a name for the **DB Instance Identifier**.

![RDS Encrypted Snapshot Identifier Name](/docs/LAB%206%20RDS%20Data%20Encryption/img/encryptedRestoredSnapshotIdentifierName.png)


#### 14. Enable Public Access for the Restored Snapshot
- In the **Connectivity** section, select **Public Access** as **Yes**.

![RDS Encrypted Snapshot Public Access](/docs/LAB%206%20RDS%20Data%20Encryption/img/connectivityPublicAccess.png)


#### 15. Restore DB Instance
- Click on **Restore DB Instance** and wait for the database to be created from the snapshot.

![RDS Encrypted Database Being Created](/docs/LAB%206%20RDS%20Data%20Encryption/img/encryptedDatabaseCreated.png)