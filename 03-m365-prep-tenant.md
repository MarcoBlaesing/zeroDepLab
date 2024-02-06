# Prepare your Microsoft Office 365 tenant

   ![m365-dev](images/03/m365.png "Prep M365 Dev")

## Sign into your Microsoft Office 365 tenant

1. Log in to the portal at https://admin.microsoft.com

1. Click **Sign in**.

    ![m365-dev](images/03/m365-prep01.png "Prep M365 Dev")

1. Enter your username. You’ll need to use the format below:

> Note: **username@your demo domain.onmicrosoft.com**

1. Click **Next**.

    ![m365-dev](images/03/m365-prep02.png "Prep M365 Dev")

1. Enter password and click **Sign in**.

    ![m365-dev](images/03/m365-prep03.png "Prep M365 Dev")

1. You may see this screen. If so, click **Skip for now**.

> Note: You don’t want to set up Multi-factor authentication in Microsoft because you’re going to enable it in Okta instead.  In the next section, there are instructions on disabling MFA in M365 which will prevent this from showing again.

   ![m365-dev](images/03/m365-prep04.jpg "Prep M365 Dev")
   
   You are now signed into your M365 admin interface. 


## Disable native MFA

In your demonstration environment, you will connect your Okta tenant with this Microsoft 365 tenant. All access to Microsoft 365 will be via Okta and Okta will be responsible for user authentication, registration of additional authentication factors, and enforcing Multi-Factor Authentication in line with configured authentication policy.
To stop Microsoft 365 from ALSO trying to perform MFA registration, and enforce MFA at login, you need to disable Multi-Factor Authentication in the M365 Administration pages.

1. You should already be signed in to the admin interface of your Microsoft Office 365 tenant. If not navigate to https://admin.microsoft.com and sign in.

   ![m365-dev](images/03/m365-prep05.png "Prep M365 Dev")

1. In the admin center, type **1. identity** into the search bar and select **2. Identity** from the result.

1. Click **Skip for now** if prompted to secure your account.

   ![m365-dev](images/03/m365-prep06.png "Prep M365 Dev")

     
    1. You should already be on the **Overview** page.
    1. Select the **Properties** tab.
    1. Click **Manage security defaults**.
    1. Set Security defaults to **Disabled**.
    1. Select a reason (it doesn’t matter which one you pick)
    1. Click **Save**.
  
   ![m365-dev](images/03/m365-prep07.png "Prep M365 Dev")

1. Click the **Disable** button to confirm.
   
   OK, that’s done.  Users will no longer be prompted to register for Multi-Factor Authentication by M365.  This will be handled by Okta (once you have integration set up).
   

## Add a domain for fedaration

In a Microsoft Office 365 tenant, single sign-on using an Identity Provider, such as Okta, cannot be enabled for the default “onmicrosoft.com” domain.  Before you can set up single sign-on, you must add an additional domain to your Microsoft 365 tenant. This can be a custom (your own domain) but also an additional **onmicrosoft.com** doamin.

In this section we will add an **onmicrosoft.com** domain.

### Start the Add Domain wizard

Follow these steps to add your DNS domain:

1. Navigate to Entra admin center domain names setup section: https://entra.microsoft.com/#blade/Microsoft_AAD_IAM/DomainsListBlade
   
   ![m365-dev](images/03/m365-prep08.png "Prep M365 Dev")

1. Click on **1. Add custom domain** and the enter **2. your domain name of choice**. Whatever you choose here it must end with **.onmicrosoft.com**. Finally click on **3. Add domain**.

   ![m365-dev](images/03/m365-prep09.png "Prep M365 Dev")

Your initial Microsoft Office 365 tenant setup and configuration is now complete. You are ready to integrate with Okta for Single-Sign-On and Provisioning.
