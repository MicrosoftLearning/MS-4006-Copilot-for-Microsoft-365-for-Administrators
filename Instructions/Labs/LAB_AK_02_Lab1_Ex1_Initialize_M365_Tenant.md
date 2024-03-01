## WWL Tenants - Terms of Use

If you are being provided with a tenant as a part of an instructor-led training delivery, please note that the tenant is made available for the purpose of supporting the hands-on labs in the instructor-led training. 

Tenants should not be shared or used for purposes outside of hands-on labs. The tenant used in this course is a trial tenant and cannot be used or accessed after the class is over and are not eligible for extension. 

Tenants must not be converted to a paid subscription. Tenants obtained as a part of this course remain the property of Microsoft Corporation and we reserve the right to obtain access and repossess at any time. 

# Learning Path 1 - Lab 1 - Exercise 1 - Initialize your Microsoft 365 Tenant 

Adatum Corporation is a subsidiary of Contoso Electronics. Adatum runs its legacy applications (such as Microsoft Exchange Server 2019) in an on-premises deployment. However, it recently subscribed to Microsoft 365, thereby creating a hybrid deployment in which it must synchronize its on-premises and cloud deployments. 

As Adatum's Microsoft 365 administrator, you have been tasked with preparing Adatum's Microsoft 365 deployment for Copilot for Microsoft 365. In this exercise, you will set up Adatum's Microsoft 365 trial tenant, and your instructor will guide you on how to obtain your Microsoft 365 credentials in your lab-hosted environment. You will use these credentials throughout the remaining labs in this course. 

In your lab environment, your lab hosting provider has already obtained a Microsoft 365 trial tenant for you. Your lab provider has also created two admin accounts that you will use in your VM lab environment: 

- A local administrator account for Adatum's on-premises environment (Adatum\Administrator).
- A default tenant admin account in Microsoft 365 (the display name for this user account is MOD Administrator). 

You will log into the Client 1 PC (LON-CL1) using the local Adatum\Administrator account. When you access Microsoft 365 for the first time, you will initially log in using the Microsoft 365 tenant admin account (MOD Administrator). You will then prepare Adatum's Microsoft 365 tenant for Microsoft Entra ID and for later labs using audit alerts, Microsoft Graph PowerShell, and sensitivity labels.


### Task 1 - Obtain Your Microsoft 365 Credentials

Once you launch the lab, you'll be able to access the free Microsoft 365 trial tenant provided by your lab hosting provider in the Microsoft Virtual Lab environment. Within this tenant, your lab hosting provider has created a Microsoft 365 user account for a default tenant administrator named MOD Administrator. Your lab hosting provider has assigned this user account a unique username and password, and the account has been assigned the Microsoft 365 Global administrator role. You must retrieve this username and password so that you can sign into Microsoft 365 within the Microsoft Virtual Lab environment. You will also be assigned a tenant name and tenant prefix. You will also use this information in various tasks throughout the labs for this course.

Because this course can be offered by learning partners using any one of several authorized lab hosting providers, the actual steps involved to retrieve the UPN name and tenant ID associated with your tenant may vary by lab hosting provider. Therefore, your instructor will provide you with the necessary instructions on how to retrieve this information for your course. <br/>

You should write down the following information (provided by your instructor) for later use:

- **Tenant prefix.** This tenant prefix is for the Microsoft 365 user accounts that you will use to sign into Microsoft 365 throughout the labs in this course. The domain for each Microsoft 365 user account is in the format of {user alias}@xxxxxZZZZZZ.onmicrosoft.com, where xxxxxZZZZZZ is the tenant prefix. It consists of two parts - your lab hoster's prefix (xxxxx; some hosters use a generic prefix such as M365x, while others use their company initials or some other designation) and the tenant ID (ZZZZZZ; usually a 6 digit number). Record this xxxxxZZZZZZ tenant prefix value for later use. When any of the lab steps direct you to sign into Microsoft 365 as one of the user accounts (such as the MOD Administrator), you must enter the xxxxxZZZZZZ value that you obtained here as the tenant prefix portion of your .onmicrosoft.com domain.

- **Tenant password.** This is the password provided by your lab hosting provider for the tenant admin account. **Note:** You will use this password not only for the tenant admin account, but for each of the predefined user accounts that are used throughout the labs.

- **Custom Domain name.** Your lab hosting provider has created a custom domain name for Adatum. You will use this domain when adding a custom domain into Microsoft 365 in a later lab exercise. The domain name is in the format **xxxUPNxxx.xxxCustomDomainxxx.xxx.** You must replace **xxxUPNxxx** with the UPN number provided by your lab hosting provider, and you must replace **xxxCustomDomainxxx.xxx** with the lab hosting provider's domain name. For example, let's assume your lab hosting provider is Fabrikam Inc. If the UPN number it assigns to your tenant is AMPVU3a and its custom domain name is fabrikam.us, then the domain name for your new custom domain would be AMPVU3a.fabrikam.us. Your instructor will provide you with your lab hosting provider's UPN number and custom domain name.  


### Task 2- Set up Adatum's Organization Profile

Throughout the labs in this course, you will role-play by taking on the persona of Holly Dickson, Adatum’s Microsoft 365 Administrator. In your role as Holly, you have been tasked with setting up the company’s profile for its Microsoft 365 trial tenant. In this task, you will configure the required options for Adatum’s tenant. Since Holly has yet to create a personal Microsoft 365 user account for herself (you will do this in the next lab exercise), Holly will initially sign into Microsoft 365 using the default Microsoft 365 tenant admin account and password that was created by your lab hosting provider. This account is the MOD Administrator account, whose alias is "admin". The username for this account is admin@xxxxxZZZZZZ.onmicrosoft.com (where xxxxxZZZZZZ is the tenant prefix assigned by your lab hosting provider); the display name for this account will be MOD Administrator.

1. When you open your lab hosting provider's Virtual Machine environment, you need to begin with the Client 1 VM (LON-CL1). If your VM environment opens with one of the other machines (such as LON-DC1), then switch to **LON-CL1** now.

2. Log into **LON-CL1** as the local **Administrator** account that was created by your lab hosting provider with the password **Pa55w.rd**. 

3. On the taskbar at the bottom of your screen, select the **Microsoft Edge** icon. If necessary, maximize your browser window when it opens.

4. In your Edge browser, go to the **Microsoft 365 Home** page by entering the following URL in the address bar: **https://portal.office.com** 

5. In the **Sign in** dialog box, copy and paste in the **Microsoft 365 Tenant Username** provided by your lab hosting provider (this is the MOD Administrator account). The username should be in the form of **admin@xxxxxZZZZZZ.onmicrosoft.com**, where xxxxxZZZZZZ is the tenant prefix assigned by your lab hosting provider. Select **Next**.

6. In the **Enter password** dialog box, copy and paste in the unique **Microsoft 365 Tenant Password** provided by your lab hosting provider and then select **Sign in**.

7. On the **Stay signed in?** dialog box, select the **Don’t show this again** check box and then select **Yes.** On the **Save password** dialog box that appears, select **Never**.

8. If a **Welcome to Microsoft 365** dialog box appears in the middle of the screen, there's no option to close it. Instead, to the right of the window, select the forward arrow icon (**>**) two times and then select the check mark icon to advance through the slides in this messaging window. 

9. If a **Find more apps** window appears, select the **X** in the upper right-hand corner of the window to close it. 

10. The **Welcome to Microsoft 365** page appears in your Edge browser in the **Home | Microsoft 365** tab. This is the MOD Administrator's Microsoft 365 home page. <br/>

	Notice the initials **MA** that appear in a circle in the top-right corner of the screen. These are the initials of the **MOD Administrator** account, which is the tenant admin account created by your lab hosting provider that you just signed in as. The other existing Microsoft 365 user accounts that were created by your lab hosting provider have a picture associated with each of their accounts; therefore, when you sign in as any of those users in later labs, the user's picture will be displayed rather than the user's initials. However, when a user such as the MOD Administrator has no picture assigned to it, the user's initials are displayed in place of the picture. <br/>

	On the **Welcome to Microsoft 365** page, in the list of application icons that appear in the left-hand pane, select **Admin**; this opens the **Microsoft 365 admin center** in a new browser tab. 

11. In the **Microsoft 365 admin center**, select **Show all** in the left-hand navigation pane and then select **Settings**. In the **Settings** group, select **Org settings**. 

12. On the **Org settings** page, the **Services** tab is displayed by default. Select the **Organization profile** tab.

13. In the **Organization profile** tab, select **Organization information** from the list of profile data.

14. In the **Organization information** pane that appears, enter the following information: <br/>

    - Name: **Adatum Corporation** (Note: Adatum Corporation is a subsidiary of Contoso Inc. The Microsoft trial tenant that your lab hosting provider obtained for this lab may have been originally assigned to Contoso. If **Contoso** (or any other value) appears as the organization name, then change it to **Adatum Corporation**.)

    - Street Address: **555 Main Street**

    - City: **Redmond**

    - State or province: **Washington**

    - ZIP or postal code: **98052**

    - Phone: do not change

    - Technical contact: do not change

    - Preferred language: **English**

15. Select **Save**.

16. At the top of the **Organization information** pane, note the message indicating the changes have been saved. Select the **X** in the upper right-hand corner to close the pane.

17. Remain logged into **LON-CL1** with Microsoft Edge open to the **Microsoft 365 admin center** for the next task.


### Task 3 – Install Microsoft Graph PowerShell 

Microsoft Graph PowerShell is required to perform several configuration tasks when installing Microsoft 365. Because future lab exercises will perform several of these tasks using Windows PowerShell, you should begin by installing the Microsoft Graph PowerShell module. This module allows you to perform many of the Microsoft 365 user and organization administration tasks through PowerShell. It’s great for bulk tasks such as password resets, password policies, license management and reporting, and so on.  

1. On LON-CL1, you should still be logged in as the local **adatum\administrator** account. To install Microsoft Graph PowerShell, you must open an elevated instance of **Windows PowerShell**. Type **power** in the Search box that appears in the bottom left corner of the taskbar. In the list of search results, right-click on **Windows PowerShell** (do not select Windows PowerShell ISE) and select **Run as administrator** in the drop-down menu that appears. 

2. Maximize your PowerShell window. In **Windows PowerShell**, type the following command at the command prompt to install the Microsoft Graph PowerShell module from the PowerShell Gallery and then press Enter: <br/>

		Install-Module Microsoft.Graph -Scope CurrentUser

3. You will be prompted to confirm whether you want to install the module from an untrusted repository (PSGallery). Enter **A** to select **[A] Yes to All** and then press Enter.  <br/>

    **Note:** Your response will initiate the installation of all the Microsoft Graph sub-modules. Once all the installation messages (for each sub-module) have finished displaying, it will still take approximately 5 to 10 additional minutes to complete the Microsoft Graph PowerShell installation. During this time, the cursor will continue to blink below the untrusted repository message. This may be a good time to take a short break.

4. A command prompt will appear once Microsoft Graph PowerShell has been installed. You will now display the list of sub-modules that were installed. To do so, run the following command:

		Get-InstalledModule Microsoft.Graph.* | select *name*

5. Verify the list of installed sub-modules includes the following three sub-modules that will be used in later lab exercises: 

	- Microsoft.Graph.Groups
	- Microsoft.Graph.Identity.DirectoryManagement
 	- Microsoft.Graph.Users
  	
    If all three sub-modules appear in the list of installed sub-modules, then proceed to the next step. However, if any of these three sub-modules do not appear in the list, then run the following PowerShell command to manually install the missing sub-module:

		Install-Module -Name <module name>

    For example, if the Microsoft.Graph.Identity.DirectoryManagement module did not install, then you would run the following command:

		Install-Module -Name Microsoft.Graph.Identity.DirectoryManagement

6. PowerShell's execution policy settings dictate what PowerShell scripts can be run on a Windows system. Setting this policy to **Unrestricted** enables Holly to load all configuration files and run all scripts. At the command prompt, type the following command, and then press Enter:   <br/>

		Set-ExecutionPolicy unrestricted

	‎If you are prompted to verify that you want to change the execution policy, enter **A** to select **[A] Yes to All.** 

7. Leave your PowerShell window open as you will use it in the next task.

### Task 4 – Turn on Audit Logging to enable Alert Policies

In Lab 1, Exercise 3, you will create Alert Policies using the Microsoft Defender portal. However, before you can implement alerts, an administrator must first turn on Audit Logging for the organization. Since it can take an hour or so for audit logging to become fully enabled once you turn it on, you will turn it on in this lab so that it's fully enabled by the time you get to Lab 1, Exercise 3.

1. You should still be logged into LON-CL1 as the local **adatum\administrator** account, and you should still have Windows PowerShell open from the prior task. If you closed PowerShell at the end of the prior task, then open it again using the **Run as administrator** option. 

2. In your PowerShell window, run the following command to install the Exchange Online Management module, which contains the cmdlet to turn on audit logging:

		Install-Module ExchangeOnlineManagement

3. You will be prompted to confirm whether you want to install the module from an untrusted repository (PSGallery). Enter **A** to select **[A] Yes to All** and then press Enter.

4. A command prompt will appear once the Exchange Online Management module has been installed. Run the following command to connect to the module:

		Connect-ExchangeOnline

5. A **Sign in** window will appear requesting your credentials. Enter the MOD Administrator account provided by your lab hosting provider (**admin@xxxxxZZZZZZ.onmicrosoft.com**; where xxxxxZZZZZZ is the tenant prefix provided by your lab hosting provider) and then select **Next**. On the **Enter password** window, enter the tenant admin password provided by your lab hosting provider and then select **Sign in**.

6. Run the following command to turn on audit logging:

		Set-AdminAuditLogConfig -UnifiedAuditLogIngestionEnabled $true

    **Note:** A warning message will be displayed indicating the admin audit log condiguration change that you requested could take up to 60 minutes to take effect throughout the system. This is why you're enabling this feature now rather than waiting for the Alert Policy labs later in this course. 

7. Run the following command to confirm that audit logging is enabled:

		AdminAuditLogConfig 

    In the list of properties that's displayed, verify the **UnifiedAuditLogIngestionEnabled** property is set to  **True**.

8. Do **NOT** close your PowerShell window. Leave the Windows PowerShell window open but minimize it for now. Remain logged into LON-CL1 and keep your Edge browser open.


### Task 5 - Run a PowerShell script to create and publish a sensitivity label

In this task, you will run a lab setup script that creates a sensitivity label and sensitivity label policy for future use in this lab series. Running this script is necessary to support the lab that you will perform on the last day of class to create a sensitivity label and label policy. The sensitivity label lab basically consists of two parts: 1) Creating a label and publishing a label policy, and 2) Testing the published label policy. The problem with the sensitivity label lab is that once you publish a label policy, it takes 24 hours for the published label policy to propagate through Microsoft 365. As such, you won't be able to test the label and policy that you create and publish on the last day of class. 

To address this timing issue, you will run a PowerShell script in this task that creates a sensitivity label and publishes it to a label policy. By the time you get to the last day of class, this label policy will have propagated through the system, and you'll be able to test it. 

**Note:** In the sensitivity label lab that you perform on the last day of class, you will create another label and label policy - just ones with different names. Their settings will be exactly the same as the ones created by this script. The sensitivity label lab will give you the experience of creating a label and publishing a label policy using the Microsoft 365 UI. However, when you perform the tasks to test the sensitivity label and label policy, you won't test the ones that you created and published in the UI, since they won't be available for testing until the next day. Instead, you will test the label and label policy that were created and published using the script that you run in this task. 

1. On **LON-CL1**, select the **File Explorer** icon from the Windows taskbar. Maximize the File Explorer window.

2. In **File Explorer**, navigate to the following folder location: **C:\Users\Administrator.ADATUM\Documents\Lab Setup**.

3. In the **Lab Setup** subfolder a .bat file named **LabSetup.bat** should exist.

    Right-click on the **LabSetup.bat** file and then select **Run as administrator**. Doing so will start the lab setup process.

    **Note:** If a **Windows protected your PC** pop-up warning is displayed, select **More info** and then select **Run anyway** at the bottom of the pop-up to continue. A **Lab setup** window will appear on the screen.

4. It may take up to 1 minute before a **Pick an account** window appears. Select the administrator account provided by your lab hosting provider (**admin@xxxxxZZZZZZ.onmicrosoft.com**; where xxxxxZZZZZZ is the tenant prefix provided by your lab hosting provider) and then select **Next**. On the **Enter password** window, enter the tenant admin password provided by your lab hosting provider and then select **Sign in**.

5. A **Pick an account** window will appear. On this window, select **MOD Administrator** from the list of available accounts. If prompted, enter the tenant admin password provided by your lab hosting provider and then select **Sign in**.

    **Important:** The **Lab Setup** process has a time-out of 5 minutes. If you fail to type in your credentials within this 5 minute time frame, a pop-up message displaying **Lab Setup Failed. EXITING...** will appear. Select **Ok**, close the Microsoft Sign-on window, and repeat steps 3-5.

6. Once the lab setup process has completed, a pop-up message displaying **Lab Setup Completed. EXITING...** will appear. Select **Ok** and proceed.

    **Note:** It may take up to 5 minutes for the lab setup process to complete.

Congratulations! You have completed all the steps to initialize your lab tenant. You are now ready to perform the remaining lab exercises.

# End of Lab 1
