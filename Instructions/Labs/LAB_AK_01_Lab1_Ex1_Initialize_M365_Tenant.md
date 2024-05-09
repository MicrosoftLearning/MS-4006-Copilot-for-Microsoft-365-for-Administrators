## WWL Tenants - Terms of Use

If you are being provided with a tenant as a part of an instructor-led training delivery, please note that the tenant is made available for the purpose of supporting the hands-on labs in the instructor-led training. 

Tenants should not be shared or used for purposes outside of hands-on labs. The tenant used in this course is a trial tenant and cannot be used or accessed after the class is over and are not eligible for extension. 

Tenants must not be converted to a paid subscription. Tenants obtained as a part of this course remain the property of Microsoft Corporation and we reserve the right to obtain access and repossess at any time. 

# Learning Path 1 - Lab 1 - Exercise 1 - Initialize your Microsoft 365 Tenant 

Adatum Corporation is a subsidiary of Contoso Electronics. Adatum runs its legacy applications (such as Microsoft Exchange Server 2019) in an on-premises deployment. However, it recently subscribed to Microsoft 365, thereby creating a hybrid deployment in which it must synchronize its on-premises and cloud deployments. 

As Adatum's Microsoft 365 administrator, you have been tasked with deploying Microsoft 365 in Adatum’s hybrid deployment using a virtualized lab environment. In this exercise, you will set up Adatum's Microsoft 365 trial tenant, and your instructor will guide you on how to obtain your Microsoft 365 credentials in your lab-hosted environment. You will use these credentials throughout the remaining labs in this course. 

In your lab environment, your lab hosting provider has already obtained a Microsoft 365 trial tenant for you. Your lab provider has also created two admin accounts that you will use in your VM lab environment: 

- A local administrator account for Adatum's on-premises environment (Adatum\Administrator).
- A default tenant admin account in Microsoft 365 (the display name for this user account is MOD Administrator). 

You will log into the Client 1 PC (LON-CL1) using the local Adatum\Administrator account. When you access Microsoft 365 for the first time, you will initially log in using the Microsoft 365 tenant admin account (MOD Administrator). You will then prepare Adatum's Microsoft 365 tenant for Microsoft Entra ID and for later labs using audit alerts and Microsoft Graph PowerShell.

**Important MFA Announcement:** Microsoft Security has recently employed a new security firewall in the trial tenants that are used in its training courses. This feature requires that all trial tenants used by Microsoft World-Wide Learning employ Multifactor Authentication (MFA) each time a user signs into Microsoft 365. Microsoft World-Wide Learning can NOT turn off this security requirement in its training labs. In addition, we can't use Conditional Access to turn MFA on or off for selected groups of users. MFA will be turned on for everyone and can never be turned off. Any time you sign in to Microsoft 365 in this trial tenant as one of the fictitious users, you must sign in with the user's account and password AND with a second form of authentication. Your instructor will guide you through the MFA process that's currently employed in the tenant.


### Task 1 - Obtain Your Microsoft 365 Credentials

Once you launch the lab, you'll be able to access the free Microsoft 365 trial tenant provided by your lab hosting provider in the Microsoft Virtual Lab environment. Within this tenant, your lab hosting provider has created a Microsoft 365 user account for a default tenant administrator named MOD Administrator. Your lab hosting provider has assigned this user account a unique username and password, and the account has been assigned the Microsoft 365 Global administrator role. You must retrieve this username and password so that you can sign into Microsoft 365 within the Microsoft Virtual Lab environment. You will also be assigned a tenant name and tenant prefix. You will also use this information in various tasks throughout the labs for this course.

Because this course can be offered by learning partners using any one of several authorized lab hosting providers, the actual steps involved to retrieve the UPN name and tenant ID associated with your tenant may vary by lab hosting provider. Therefore, your instructor will provide you with the necessary instructions on how to retrieve this information for your course. <br/>

You should make note of the following information provided by your lab hosting provider for later use:

- **Administrative Username.** When a company purchases a Microsoft 365 subscription, Microsoft creates a default administrator account in the company's tenant and assigns it the Global Administrator role. The person who signs up for the Microsoft 365 subscription is typically the one who gets assigned this default Global administrator account. In this trial tenant, your lab hosting provider assigned the MOD Administrator name, the **Administrative Username** and **Administrative Password** to this account. The Administrative Username assigned to this account is **admin@{tenant name}**. 

- **Administrative Password.** This is the password that your lab hosting provider assigned to the **MOD Administrator** account. Later in this lab, you will create another Global Administrator account for **Holly Dickson**. For the sake of expediency in the lab, you will assign this same **Administrative Password** to Holly's account. Only Holly and the MOD Administrator will use this **Administrative Password**.

- **Tenant name.** This is the tenant domain of the trial tenant that was assigned to your VM lab environment. You will use this tenant name when signing into Microsoft 365 and PowerShell as various user accounts throughout the labs in this course. The tenant name is in the format **xxxxxZZZZZZ.onmicrosoft.com**, where xxxxxZZZZZZ is the tenant prefix and onmicrosoft.com is the domain name. The domain name is the domain associated with your Microsoft 365 services. When any of the lab steps direct you to sign into Microsoft 365 or PowerShell as one of the user accounts, you must enter the user's alias followed by this tenant name. For example, if your tenant prefix was WWLx123456, then when signing in as Holly Dickson, you would enter Holly@WWLx123456.onmicrosoft.com.

- **Tenant prefix.** The domain for each Microsoft 365 user account is in the format of {user alias}@xxxxxZZZZZZ.onmicrosoft.com, where xxxxxZZZZZZ is the tenant prefix. It consists of two parts - your lab hoster's prefix (xxxxx; some hosters use a generic prefix such as M365x, while others use their company initials or some other designation, such as WWLx) and the tenant ID (ZZZZZZ; usually a 6 digit number). 

 - **User Password.** Your trial tenant includes a number of predefined user accounts. One of those accounts is the MOD Administrator, who's the Global admin account that was created for your trial tenant. Your lab hosting provider assigned the **Administrative Password** to this account. The **User Password**, on the other hand, is the password that your lab hosting provider assigned to all the other predefined user accounts that it created. So all the other predefined user accounts that are in the **Active Users** list - many of which you'll use throughout the labs in this course - have all been assigned this **User Password**. You must use this password when signing in as any of these users, such as Alex Wilber, Joni Sherman, Lynne Robbins, and so on.


### Task 2- Set up Adatum's Organization Profile

Throughout the labs in this course, you will role-play by taking on the persona of Holly Dickson, Adatum’s Microsoft 365 Administrator. In your role as Holly, you have been tasked with setting up the company’s profile for its Microsoft 365 trial tenant. In this task, you will configure the required options for Adatum’s tenant. Since Holly has yet to create a personal Microsoft 365 user account for herself (you will do this in the next lab exercise), Holly will initially sign into Microsoft 365 using the default Microsoft 365 tenant admin account and password that was created by your lab hosting provider. This account is the **MOD Administrator** account, whose alias is "admin". The username for this account is **admin@xxxxxZZZZZZ.onmicrosoft.com** (where xxxxxZZZZZZ is the tenant prefix assigned by your lab hosting provider); the display name for this account will be MOD Administrator.

1. When you open your lab hosting provider's Virtual Machine environment, you need to begin with the Client 1 VM (LON-CL1). If your VM environment opens with one of the other machines (such as LON-DC1), then switch to **LON-CL1** now.

2. Log into **LON-CL1** as the local **Administrator** account that was created by your lab hosting provider with the password **Pa55w.rd**. 

3. On the taskbar at the bottom of your screen, select the **Microsoft Edge** icon. If necessary, maximize your browser window when it opens.

4. In your Edge browser, go to the **Microsoft 365 Home** page by entering the following URL in the address bar: **https://portal.office.com** 

5. In the **Sign in** dialog box that appears, enter the **Administrative Username** provided by your lab hosting provider (this is the MOD Administrator account). The username should be in the form of **admin@xxxxxZZZZZZ.onmicrosoft.com**, where xxxxxZZZZZZ is the tenant prefix assigned by your lab hosting provider. Select **Next**. <br/>

	**Note:** Your lab hosting provide may provide the ability to select a **Type text** (or equivalent) button next to resource data such as usernames, passwords, PowerShell commands, and other data that must be entered throughout the course of these labs. Other lab hosting providers may provide an alternative method, such as the ability to copy and paste in this information. Take advantage of this functionality to save yourself from having to manually enter this information. 

6. In the **Enter password** dialog box, enter the unique **Administrative Password** provided by your lab hosting provider and then select **Sign in**. If required, complete the MFA sign-in process.

7. On the **Stay signed in?** dialog box, select the **Don’t show this again** check box and then select **Yes.** On the **Save password** dialog box that appears, select **Never**.

8. If a **Welcome to Microsoft 365** dialog box appears in the middle of the screen, there's no option to close it. Instead, to the right of the window, select the forward arrow icon (**>**) two times and then select the check mark icon to advance through the slides in this messaging window. 

9. If a **Find more apps** window or a **Create with Microsoft 365** window appears, select the **X** in the upper right-hand corner of the windows to close them. 

10. The **Welcome to Microsoft 365** page appears in your Edge browser in the **Home | Microsoft 365** tab. This is the MOD Administrator's Microsoft 365 home page. <br/>

	Notice the icon that appears in the top-right corner of the screen. This icon represents the **MOD Administrator** account, which is the tenant admin account created by your lab hosting provider that you just signed in as. The other existing Microsoft 365 user accounts that were created by your lab hosting provider have a picture associated with each of their accounts; therefore, when you sign in as any of those users in later labs, the user's picture will be displayed rather than the user's initials. However, when a user such as the MOD Administrator has no picture assigned to it, either the user's initials are displayed in place of the picture, or as in this case, an icon that was assigned to the account. <br/>

	On the **Welcome to Microsoft 365** page, in the list of application icons that appear in the left-hand pane, select **Admin**; this opens the **Microsoft 365 admin center** in a new browser tab. 

11. In the **Microsoft 365 admin center**, select **Show all** in the navigation pane and then select **Settings**. In the **Settings** group, select **Org settings**. 

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

### Task 3- Create a custom theme for Adatum's pilot project team

In the prior task, you learned that when someone is signed into Microsoft 365, the system will either display their photograph (if one is supplied), or their initials if no photograph is provided. Holly Dickson, Adatum's Microsoft 365 Administrator, is not satisfied with just seeing a picture or initials of the signed-in user. She wants to create a custom theme for the members of her pilot project team so that it also displays the signed-in user's name. At the end of the pilot project, if the pilot project team members prefer this design, she will configure this same option in the default theme so that it applies to all users. 

Custom themes must be associated with one or more Microsoft 365 groups. Therefore, to implement this change, Holly must first create a Microsoft 365 group for the members of the pilot project team. She can then create a custom theme associated with this group that enables the setting to display the signed-in user's name. In this task, you will create a Microsoft 365 group for the members of Adatum's Microsoft 365 pilot project team. You will then create a custom theme that displays the signed-in user's name, and you will assign the pilot project team to this theme. You will also review other options that can be configured with custom themes, and you can make any color changes that you wish.

**Important:** At the end of this task, you will attempt to save the custom theme that you created. There is a known platform issue in the Microsoft 365 admin center where sometimes it saves the custom theme just fine, and other times it returns a message that says "Sorry, we couldn't save your theme. Please try again later." If you receive this message, there's nothing you can do but move on. Trying to save the theme at a later time usually returns the same error. This issue won't affect any future labs, other than it won't display the user's name next to their user icon or initials on the heading line. Despite this known issue, we still want you to perform this task to gain experience in creating a theme, even though it may not get saved in your trial tenant.

1. You should still be logged into LON-CL1 as the local **adatum\administrator** account, and in your Edge browser, you should still be logged into Microsoft 365 as the **MOD Administrator**. 

2. In the **Microsoft 365 admin center**, select **Teams & groups** in the navigation pane, and then under it, select **Active teams & groups**. 

3. In the **Active teams and groups** page, there's a tab for viewing each of the group types. The **Teams & Microsoft 365 groups** tab is displayed by default. This tab displays the existing Microsoft 365 groups.  <br/>

    Select the **+Add a Microsoft 365 group** option that appears on the menu bar above the list of Teams and Microsoft 365 groups. This initiates the **Add a Microsoft 365 group** wizard. 

4. In the **Add a Microsoft 365 group** wizard, on the **Set up the basics** page, enter **M365 pilot project** in the **Name** field, and then enter **Members of the Microsoft 365 pilot project team** in the **Description** field (Note: even if you don't enter a description, you must still select into this field to enable the **Next** button). Select **Next**.

5. You will now assign the MOD Administrator as owner of the **M365 pilot project** group. In the **Assign owners** window, select **+Assign owners**.
	
6. In the **Assign owners** pane that appears, select the check box next to **MOD Administrator**, and then select the **Add (1)** button at the bottom of the pane.

7. On the **Assign owners** page, MOD Administrator should appear as owner of the group. Select **Next**.

8. You will now assign members to the M365 pilot project group. In the **Add members** page, select **+Add members**.

9. In the **Add members** pane that appears, select the check boxes next to the following users (in alphabetical order): **Alex Wilber**, **Allan Deyoung**, **Diego Siciliani**, **Isaiah Langer**, **Joni Sherman**, **Lynne Robbins**, **Megan Bowen**, **MOD Administrator**, **Nestor Wilke**, and **Patti Fernandez**. Then select the **Add (10)** button at the bottom of the pane.

10. On the **Add members** page, verify these 10 users are listed as members of the group. If you missed a user, select **+Add members** and then add any of the 10 users that you missed. When all 10 users appear on this page, select **Next**.

11. In the **Edit settings** page, enter the following information: <br/>

	- Enter **m365pilotproject** in the **Group email address** field.
	- In the **Privacy** field, select **Private**.
	- Under the **Add Microsoft Teams to your group** section, verify the **Create a team for this group** check box is selected (select it if it's blank), and then select **Next**.

12. In the **Review and finish adding group** page, review the content that you entered. If anything needs to be fixed, select **Edit** under the specific area that needs adjustment, make any necessary corrections, and then select **Next** to continue back to this page. Once everything is correct, select **Create group**.

13. Once the **M365 pilot project group created** window appears, note the comment at the top of the page that it may take 5 minutes for the new group to appear in the list of Active groups.  </br>

	Select **Close**. This returns you to the **Active teams and groups** page, which should display the **Teams & Microsoft 365 groups** tab. Since the M365 pilot project group was a Microsoft 365 group, it should eventually display on this tab. If necessary, select the **Refresh** option on the menu bar until you see the M365 pilot project group in the list of Teams and Microsoft 365 groups.

14. In the **Microsoft 365 admin center**, select **Settings** in the navigation pane and then select **Org settings**. 

15. On the **Org settings** page, the **Services** tab is displayed by default. Select the **Organization profile** tab.

16. The **Organization profile** tab displays the list of organization profile data. In the list of data, select **Custom themes**.

17. In the **Customize Microsoft 365 for your organization** pane that appears, you can customize the default theme that users see when signed into Microsoft 365, and you can add additional custom themes. You want to create a new custom theme that applies only to the members of the **M365 pilot project** group that you previously created, so select the **+Add theme** option.

18. In the **New group theme** pane that appears, the **General** tab is displayed by default. Enter **M365 pilot project theme** in the **Name** field.

19. Select inside the **Groups** field. In the list of groups that appears, select **M365 pilot project** if it appears in the list of groups. <br/>

	**Note:** If **M365 pilot project** doesn't appear in the list of groups, then enter **M365** in the **Groups** field. A search results box should appear that displays the **M365 pilot project** group. Select **M365 pilot project**. 

20. Select the **Show the user's display name** check box. This is the setting that Holly wants to customize for the M365 pilot project team members. This option displays the signed-in user's name next to their initials in each window heading.
 
21. Select the **Logos** tab and take some time to review its options. Do the same for the **Colors** tab. Note the various theme and branding options that are available for you to update. <br/>

	For the purpose of this lab, you can change any of the options or leave the default values as is. For example, in your real-world environment, you can add the logo of your company and set the background image as the default for all your users. For this lab, feel free to change the colors for your navigation pane, text color, icon color, and accent color. <br/>

	**Go ahead and explore the different options for this theme that will be used by the Microsoft 365 pilot project team members. Make any changes that you wish.** <br/>

	**Tip:** Some color patterns aesthetically distract users. If you do change any of the colors, it's recommended that you avoid using high contrasting colors together, such as neon colors and high-resolution colors like bright pink and white.

22. Select **Save**. 

	**Note:** As previously mentioned at the start of this task, there's a known platform issue in the Microsoft 365 admin center where sometimes it saves a new custom theme, and other times it returns a message that says "Sorry, we couldn't save your theme. Please try again later." If you receive this message, it won't affect any future labs. Since your custom theme didn't get save, the system simply won't display the user's name next to their user icon or initials on the heading line (plus any color changes you may have made won't appear). We still asked you to do this task even though you may receive this message in order to gain the experience of creating a theme such as this. So if you get this error, skip the next step, which tests the custom theme. However, you can still perform the remaining steps following the next step in order to learn about the Default theme. Whether or not your custom theme was saved, close the **M365 pilot project theme** pane.

23. If your custom theme did not get saved, then skip to the next step. However, if your custom theme was saved, then select the **Refresh** icon at the top of the screen, to the left of the address bar. Once the screen refreshes, note how the **MOD Administrator** name appears to the left of either the circle with the MA initials or the icon selected for this account by your lab-hosting provider. When members of the Microsoft 365 pilot project team sign in to Microsoft 365, this custom theme will display their username, just as the MOD Administrator name appears here. 

24. In the list of organization profile data, select **Custom themes**.

25. In the **Customize Microsoft 365 for your organization** pane that appears, notice how it displays the **Default theme** and the **M365 pilot project theme** (if the theme was saved in the previous step). Select the **Default theme**. 

26. On the **Default theme** pane, notice how the **Show the user's display name** option is not selected for the default theme. If Holly later decides to make the **Show the user's display name** option a permanent feature, she will select this option in the **Default theme** pane so that it applies to all Adatum users, and she will delete the **M365 Pilot project theme**. <br/>

	**Note:** If you received the "Sorry, we couldn't save your theme. Please try again later." error message when you previously tried to save your custom theme, then select this **Show the user's display name** option on the Default theme, and then select **Save**. We want you to see what happens when this option is selected, even if you couldn't save your custom theme. If you set this option on the Default theme, then select the **Refresh** icon at the top of the screen, to the left of the address bar. Once the screen refreshes, note how the **MOD Administrator** name appears to the left of either the circle with the MA initials or the icon selected for this account by your lab-hosting provider.
 
27. Close the **Default theme** pane.

28. Remain logged into **LON-CL1** with Microsoft Edge open to the **Microsoft 365 admin center** for the next task.

### Task 4 – Install Microsoft Graph PowerShell 

Microsoft Graph PowerShell is required to perform several configuration tasks when installing Microsoft 365. Because future lab exercises will perform several of these tasks using Windows PowerShell, you should begin by installing the Microsoft Graph PowerShell module. This module allows you to perform many of the Microsoft 365 user and organization administration tasks through PowerShell. It’s great for bulk tasks such as password resets, password policies, license management and reporting, and so on.  

1. On LON-CL1, you should still be logged in as the local **adatum\administrator** account. To install Microsoft Graph PowerShell, you must open an elevated instance of **Windows PowerShell**. Type **power** in the Search box that appears in the bottom left corner of the taskbar. In the list of search results, right-click on **Windows PowerShell** (do not select Windows PowerShell ISE) and select **Run as administrator** in the drop-down menu that appears. 

2. Maximize your PowerShell window. In **Windows PowerShell**, type the following command at the command prompt to install the Microsoft Graph PowerShell module from the PowerShell Gallery and then press Enter: <br/>

		Install-Module Microsoft.Graph -Scope CurrentUser

3. You will be prompted to confirm whether you want to install the module from an untrusted repository (PSGallery). Enter **A** to select **[A] Yes to All** and then press Enter.  <br/>

    **Note:** Your response will initiate the installation of all the Microsoft Graph sub-modules. Once all the installation messages for each sub-module have finished displaying, it will still take approximately 5 to 10 additional minutes to complete the Microsoft Graph PowerShell installation. During this time, the cursor will continue to blink below the untrusted repository message. <br/>

	**This may be a good time to take a short break.**

4. A command prompt will appear once Microsoft Graph PowerShell has been installed. You will now display the list of sub-modules that were installed. To do so, run the following command:

		Get-InstalledModule Microsoft.Graph.* | select *name*

5. Verify the list of installed sub-modules includes the following three sub-modules that will be used in later lab exercises: 

	- Microsoft.Graph.Groups
	- Microsoft.Graph.Identity.DirectoryManagement
 	- Microsoft.Graph.Users
  	
    If all three sub-modules appear in the list of installed sub-modules, then proceed to the next step. However, if any of these three sub-modules do not appear in the list, then run the following PowerShell command to manually install the missing sub-module:

		Install-Module -Name <module name> -Scope CurrentUser

    For example, if the Microsoft.Graph.Identity.DirectoryManagement module did not install, then you would run the following command:

		Install-Module -Name Microsoft.Graph.Identity.DirectoryManagement

6. PowerShell's execution policy settings dictate what PowerShell scripts can be run on a Windows system. Setting this policy to **Unrestricted** enables Holly to load all configuration files and run all scripts. At the command prompt, type the following command, and then press Enter:   <br/>

		Set-ExecutionPolicy unrestricted

	‎If you are prompted to verify that you want to change the execution policy, enter **A** to select **[A] Yes to All.** 

7. Leave your PowerShell window open but minimize it. You will use it in a later lab exercise.


**Congratulations! You have completed all the steps to initialize your lab tenant. You are now ready to perform the remaining lab exercises.**

# End of Lab 1
