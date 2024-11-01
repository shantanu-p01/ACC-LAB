### Step-by-Step Guide for Setting Up Amazon Cognito User Pool with Hosted UI

---

#### Step 1: Configure Sign-In Experience
1. Go to **Amazon Cognito** in the AWS Console.
2. Click **Create User Pool**.
3. In **Sign-in experience**:
   - Set **Provider Type** to **Create User Pool**.
   - Choose **Email** as the sign-in option.
   - Click **Next**.
   ![CognitoSignInExperience](/docs/Lab%208%20AWS%20Congito%20Demo/img/CognitoSignInExperience.png)

---

#### Step 2: Configure Security Requirements
1. In **Security requirements**:
   - Set **Password policy** to **Custom password**.
   ![CognitoPasswordPolicy](/docs/Lab%208%20AWS%20Congito%20Demo/img/CognitoPasswordPolicy.png)
   - Set **MFA** to **Optional** and **MFA Method** to **Authenticator Apps**.
   ![CognitoMFAConfig](/docs/Lab%208%20AWS%20Congito%20Demo/img/CognitoMFAConfig.png)
   - Enable **Self-service account recovery**.
   - For **Delivery method for user account recovery messages**, select **Email only**.
   ![CongitoUserAccountRecovery](/docs/Lab%208%20AWS%20Congito%20Demo/img/CongitoUserAccountRecovery.png)

---

#### Step 3: Enable Self-Service Sign-Up
1. Enable **Self-registration** to allow users to register themselves.
   ![CognitoSelfServiceSignUp-Enable](/docs/Lab%208%20AWS%20Congito%20Demo/img/CognitoSelfServiceSignUp-Enable.png)
2. In **Verification and confirmation**:
   - Enable **Allow Cognito to automatically send messages to verify and confirm**.
   - Choose **Send email message** to verify the email address.
   ![CognitoAttributeVerificationAndUserAccountConfirmation](/docs/Lab%208%20AWS%20Congito%20Demo/img/CognitoAttributeVerificationAndUserAccountConfirmation.png)
3. For **Attribute settings**:
   - Check **Keep original attribute value active when an update is pending** (recommended) for **Email Address**.
   ![CongitoVerifyingAttributeChanges](/docs/Lab%208%20AWS%20Congito%20Demo/img/CongitoVerifyingAttributeChanges.png)
   - In **Required attributes**, select **Name**.
   ![CognitoRequiredAttribute](/docs/Lab%208%20AWS%20Congito%20Demo/img/CognitoRequiredAttribute.png)

---

#### Step 4: Configure Message Delivery
1. Set **Email delivery** to **Send email with Cognito**.
   ![CognitoMessageDelivery](/docs/Lab%208%20AWS%20Congito%20Demo/img/CognitoMessageDelivery.png)

---

#### Step 5: Integrate Your App
1. Name your **User Pool** as desired.
   ![CognitoUserPoolName](/docs/Lab%208%20AWS%20Congito%20Demo/img/CognitoUserPoolName.png)
2. Check **Use the Cognito Hosted UI**.
   ![CognitoHostedUIChecked](/docs/Lab%208%20AWS%20Congito%20Demo/img/CognitoHostedUIChecked.png)
3. For **Domain**, select **Use a Cognito domain** and set it to `lab-7-1113`.
   ![CognitoDomain](/docs/Lab%208%20AWS%20Congito%20Demo/img/CognitoDomain.png)

---

#### Step 6: Set Up the Initial App Client
1. For **App Client**, select **Public client**.
   ![CognitoInitialAppClient](/docs/Lab%208%20AWS%20Congito%20Demo/img/CognitoInitialAppClient.png)
2. Enter a **Client name**.
   ![CognitoInitialAppClientName](/docs/Lab%208%20AWS%20Congito%20Demo/img/CognitoInitialAppClientName.png)
3. Set the **Callback URL** to `http://localhost`.
   ![CognitoCallbackUrl](/docs/Lab%208%20AWS%20Congito%20Demo/img/CognitoCallbackUrl.png)
4. Review the settings and click **Create User Pool**.

---

#### Step 7: Create a User in the User Pool
1. After creating the user pool, go to the **Users** section.
2. Click **Create User**.
   ![CongitoUsersTab](/docs/Lab%208%20AWS%20Congito%20Demo/img/CongitoUsersTab.png)
3. Choose **Do not send an invitation**.
4. Enter the user's **email address**.
5. Enable **Mark email address as verified**.
6. Set a password (e.g., `YouDontNeedToKnow`).
   ![CongitoUserCreating](/docs/Lab%208%20AWS%20Congito%20Demo/img/CongitoUserCreating.png)
7. Click **Create User**.

---

#### Step 8: Access the Hosted UI
1. Go to **App Integration** under the user pool.
   ![CongitoAppIntegrationTab](/docs/Lab%208%20AWS%20Congito%20Demo/img/CongitoAppIntegrationTab.png)
2. Scroll to the **App Integration** tab and locate **App Client List** within your user pool.
3. Click on the **App Client Name**.
   ![CognitoAppClientList](/docs/Lab%208%20AWS%20Congito%20Demo/img/CognitoAppClientList.png)

---

#### Step 9: Test the Hosted UI
1. Scroll down to the **Hosted UI** section.
2. Click **View Hosted UI**.
   ![CognitoHostedUISection](/docs/Lab%208%20AWS%20Congito%20Demo/img/CognitoHostedUISection.png)
3. Enter the email and password for the user created earlier, or create a new account.
   ![CognitoHostedUiTesting1](/docs/Lab%208%20AWS%20Congito%20Demo/img/CognitoHostedUiTesting1.png)