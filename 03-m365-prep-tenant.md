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

In your demonstration environment, you will connect your Okta tenant with this M365 tenant.  All access to M365 will be via Okta and Okta will be responsible for user authentication, registration of additional authentication factors, and enforcing Multi-Factor Authentication in line with configured authentication policy.
To stop M365 from ALSO trying to perform MFA registration, and enforce MFA at login, you need to disable Multi-Factor Authentication in the M365 Administration pages.

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
