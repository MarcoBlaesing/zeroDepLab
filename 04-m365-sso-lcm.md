# Integrate Okta for Single-Sign-On and Lifecycle Management with your Microsoft Office 365 tenant

In this lab, we'll effortlessly integrate Okta with your Microsoft Office 365 environment. By leveraging the Okta Integration Network, you'll experience firsthand how modern application integrations can be both straightforward and rapid. Through the benefits of automated provisioning and single sign-on, employees will be poised for instant productivity. And even as we focus on a user-friendly experience, remember, security is always at the forefront.

## Add an Okta Group for provisioning

1. Log in to your Okta Admin Dashboard `{{idp.name}}-admin.okta.com`
1. In the Admin Dashboard select **Directory** >  **Groups**.
1. Click **Add group**.
1. Enter **App-Office365-ProPlus** as **Name** for the new group.
1. Click **Save**.

## Add Microsoft Office 365 App to Okta for SSO

1. In the Admin Dashboard select **Applications** >  **Applications**.
1. Click **Browse App Catalog**.
1. In the Browse App Integration Catalog **Search...** bar, type *office 365* and then click **Microsoft Office 365**.
1. Click **Add integration**.

### General Settings

1. In the **General Settings** tab, enter your **Office365.Tenant.Name**

    ![App Definition Tenant Name](images/04/m365-sso01.png "App Defintion Tenant Name")
1. Optional. For **Display the following links**, deselect all but: **Word Online, Excel Online, PowerPoint Online and Office Portal**.
1. Scroll down and click **Next**.

### Sign-On Options

1. In the **Sign On Options** tab, select **WS-Federation**.

    ![WS-Federation](images/04/m365-sso02.png "WS-Federation   ")
   
1. Set the **Office 365 Admin Username** to `Office365.Admin.Username@Office365.Tenant.Name.onmicrosoft.com`
1. Set the **Office 365 Admin password** to `Office365.Admin.Password`
1. Click **Fetch and Select**. This will fetch a list of your Office 365 Domains.

    ![Fetch and Select](images/04/m365-sso03.png "Fetch and Select")

10. Select the **Office365.Domain** domain, and then click **Select**.

    ![Select Domain](images/04/m365-sso04.png "Select Domain")

### Customization with Okta Expression Language

1. In the **Credential Details** section, for **Application username format** select **Custom**.
1. For the **Custom** expression, copy and paste the following expression:

    ```javascript
    String.substringBefore(user.login,"@") + "@Office365.Domain"
    ```

    ![Custom Expression](images/04/m365-sso05.png "Custom Expression")

4. Click **Done**.

Congratulations! Your Okta Workforce Identity Cloud and Office 365 tenant are now configured for single sign-on from Okta to Office 365.

## Configure Provisioning for Office 365

For single sign-on to work, each identity asserted by Okta must link to an existing Azure AD account.

In this section, you will set up provisioning in Okta to automatically create Azure AD accounts when users are assigned to the Office 365 app and deactivate these accounts when users are unassigned.

### Enable integration

Accounts in Azure AD can be managed via Microsoft APIs. To enable provisioning, Okta must be granted authority to call these APIs. Follow the steps below to grant this access and enable integration:

1. In the **Microsoft Office 365** app definition, select the **Provisioning** tab.
1. Click **Configure API Integration**.

    ![Configure API Integration](images/04/m365-prov01.png "Configure API Integration")

1. Select **Enable API integration**.
1. Click **Authenticate with Microsoft Office 365**.

    ![Authenticate with Microsoft Office 365](images/04/m365-prov02.png "Authenticate with Microsoft Office 365")

1. Authenticate using the credentials for your Microsoft tenant from the launch pad.
1. On the **Permissions Requested** dialog, click **Accept** to grant the permissions requested by the Okta Microsoft Graph Client, and be returned to the Okta Admin Console.
1. Click **Save**.

The API connection for provisioning is now in place. Provisioning configuration is now shown under the Provisioning tab. The integration configuration you just created is under the Integration tab.

### Enable provisioning from Okta to App

In this section you will enable provisioning to Microsoft 365. This will include creation of accounts in Azure AD when users are assigned to the app, updating attributes in Azure AD when things change in Okta, and deactivating accounts in Azure AD when users are unassigned from the app in Okta.

1. On the **Provisioning** tab, under **Settings**, select **To App**.
1. Click **Edit** to set the options for provisioning from Okta to Office 365.
   
    ![Provisioning to O365](images/04/m365-prov03.png "Provisioning to O365")

1. For **Office 365 Provisioning Type**  select **Universal Sync**.
1. For **Create Users**, select **Enable**.
1. For **Update User Attributes**, select **Enable**.
1. For **Deactivate Users**, select **Enable**.
1. Click **Save**.

    ![Enable Create, Update, Deactivate](images/04/m365-prov04.png "Enable Create, Update, Deactivate")

> *Did you know that the Okta Integration Network boasts over 7,700 pre-built integrations, making it the Swiss Army knife of seamless connectivity? Integration innovation at its finest!*

## Configure group assignment

When assigning users to an app, it's common to assign a group to an app and then assign users to the group.

When assigning a group to an app, you can specify values for app attributes, such as Office 365 licenses. These will override any mapping for those attributes in the app definition. If you don't specify any value for an attribute, the mapping in the app definition will be applied instead.

## Assign Group Access to Application

You can assign a group to an app within an app definition. This will grant access to the app for all members of the group.

1. In the **Microsoft Office 365** app definition, select the **Assignments** tab.
1. Click **Assign**, and then select **Assign to Groups**.

     ![Assign to Groups](images/04/m365-prov05.png "Assign to Groups")
1. Find the **App-Office365-ProPlus** group, and then click **Assign**.
1. In the list of **Licenses**, find and select **Microsoft 365 E5 Developer (Without Windows and Audio Conferencing) - Office 365 ProPlus**. The license selection will apply to members of this group.

    >**Hint:** Command-F (on Mac) or Win+F ( on Windows) will provide you a search bar into which you can type *proplus*

     ![Office 365 ProPlus](images/04/m365-prov06.png "Office 365 ProPlus")

1. Scroll down and click **Save and Go Back**.
1. Scroll down and click **Done**.

The application is now assigned to members of the **App-Office365-ProPlus** group.

## Assign User to Group

You will now assign your user to the *App-Office365-ProPlus* group.

1. On the **Assignments** tab, select the **App-Office365-ProPlus** group.

     ![Select group](images/04/m365-prov07.png "Select Group")

1. On the **People** tab, click **Assign people**.

    ![Assign people](images/04/m365-prov08.png "Assign people")

1. Find your *new employee*, and then click the **+** icon on the right to assign them to the group.

    ![Find new employee](images/04/m365-prov09.png "Find new employee")

1. Click **Done**.

The new employee is now a member of the group and will be assigned the Microsoft Office 365 app with an E5 Developer Office Pro Plus license.

## Verify SSO for New Employee to Office 365

Test single sign-on to Microsoft Office 365 for your new employee.

1. Logout from your Okta Admin Dashbaord and close your browser
1. Open your browser, and then sign in to your **Okta** tenant with your username and password.
1. Verify that your End-User Dashboard displays the Office 365 applications.
1. Click the **Microsoft Office 365 Word Online** app.

    ![Microsoft Office 365 Word Online](images/04/m365-prov10.png "Microsoft Office 365 Word Online")

1. In the top-right corner of the page, click the identity icon.
1. Click **Sign out** to clear the session, and then close the browser tab.

    ![Sign out](images/04/m365-prov11.png "Sign out")

1. Sign out the from Okta, and then close the browser.

## Conclusion

##  :clap: Congratulations!  :clap: You have successfully configured Lifecycle Management and Single Sign-On to Microsoft Office 365. 

We hope you enjoyed this lab and hope to see you again soon. 
