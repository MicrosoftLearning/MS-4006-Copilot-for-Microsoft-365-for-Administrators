# Learning Path 2 - Lab 2 - Exercise 1 - Manage secure user access 

Organizations must ensure that access to their company data on Microsoft 365 is always secure. Microsoft 365 - and int turn, Copilot for Microsoft 365 - often displays sensitive and confidential data, including emails, documents, customer information, and intellectual property. Unauthorized access to Microsoft 365 can lead to data breaches, identity theft, and other malicious activities. By securing user access, organizations can prevent unauthorized individuals from accessing and potentially misusing or leaking company data when working in Microsoft 365 and Copilot for Microsoft 365.

In the following lab exercise, you will continue in your role as Holly Dickson, Adatum's new Microsoft 365 Administrator. You will perform several user management functions to prepare Adatum for its upcoming Copilot for Microsoft 365 deployment. You will begin by creating a Microsoft 365 user account for Holly, who will be assigned the Microsoft 365 Global Administrator role. 

**Note:** The VM environment provided by your lab hosting provider comes with over 20 existing Microsoft 365 user accounts, as well as a large number of existing on-premises user accounts. Several of the existing Microsoft 365 user accounts will be used throughout the labs in this course. Even though the MOD Administrator account has been created by your lab hosting provider, you will still create Holly Dickson's user account, since having more than one user who's assigned the Microsoft 365 Global Administrator role is a best practice. It will also provide you with the experience of creating a Microsoft 365 user account in case you're not familiar with the process.

Holly has then been asked by Adatum’s CTO to deploy Microsoft Entra Multifactor Authentication (MFA) and Microsoft Entra Smart Lockout. These features will help strengthen password management throughout the organization in preparation for Copilot for Microsoft 365. For Smart Lockout, you will deploy it using Group Policy Management. 

**IMPORTANT MFA NOTIFICATION:** Due to a recent change by Microsoft to the Microsoft 365 trial tenants used in this course, we had to make a corresponding change to this lab. <br/>

**Original lab design:** This lab exercise was originally designed so that as Holly Dickson, you created a Conditional Access policy that enabled MFA at Adatum in Task 3. This is the recommended method of enabling MFA, as you learned in the lecture portion of this training. In task 3, you created a Conditional Access policy that enabled MFA for all users, EXCEPT for those who were members of the Microsoft 365 pilot project group that you created in an earlier exercise. To test your policy in Task 4, it then had you log in as a Adele Vance. Because Adele was not a member of the pilot project group, you had to complete the MFA process to sign-in to Microsoft 365. You then signed out as Adele and signed back in as Holly Dickson. Since Holly is a member of the Microsoft 365 pilot project group, she only had to enter her username and password. She did not have to perform a second form of authentication using MFA. These two steps in Task 4 verified your Conditional Access policy - i.e.  only users who were not part of the pilot project group had to use MFA. 

The other ramification of this policy is that you didn't have to use MFA when signing in to the remainder of the labs as the other test users who were also members of the Microsoft 365 pilot project group. While exclusions from MFA can be set for practical reasons depending on a company's business needs, companies should carefully assess the associated risks and apply exclusions sparingly, always aiming to align with security best practices. This lab had you create the pilot project group exclusion for two reasons - so that you could learn how to build an exclusion into a Conditional Access policy, but also as a means of saving time in the training labs when signing in as each test user. <br/>

**Microsoft tenant change:** That being said, Microsoft has since created a Conditional Access policy in the Microsoft 365 trial tenant used in this lab that requires MFA for all user accounts. Unfortunately, Microsoft's Conditional Access policy takes precedence over the Conditional Access policy that you will create in this lab that excludes a specific group. Conditional Access policies in Microsoft Entra are evaluated together, and the highest priority policy that applies to a user is enforced. If there are multiple policies with the same priority, which is the case here, the most restrictive policy applies. In this case, Microsoft's policy is more restrictive than the policy you create, since yours includes user exceptions. <br/>

**Impact on this lab exercise:** Even though Microsoft enforces MFA in this trial tenant through a Conditional Access policy, you will still create your own Conditional Access policy as originally designed in Task 3. The task has been modified slightly from its original version so that you can see the policy that Microsoft built into the trial tenant. But other than that, the policy that you will create has not changed from its original design - it requires MFA for all users, except for the members of the Microsoft 365 pilot project group. However, since the policy that Microsoft built into the lab's trial tenant is the more restrictive of the two policies, that policy takes precedence during enforcement. There are two implications of this scenario. First, Microsoft's policy requires you to use MFA when signing in as each test user through the remainder of these labs. Second, because Microsoft Entra will ignore your policy, there's no point in testing it. As such, we removed the original Task 4 that tested the Conditional Access policy that you created. Now even though you can't test your policy, we still want you to create it in Task 3 so that you gain that experience for your real-world deployments. 

### Task 1 - Create a User Account for Adatum's Microsoft 365 Administrator

Holly Dickson is Adatum’s new Microsoft 365 Administrator. Since a Microsoft 365 user account has not been set up for her, she initially signed into Microsoft 365 as the MOD Administrator account (the default Global administrator) in the previous lab. In this task, you will continue to be logged in as the MOD Administrator, during which you will create a Microsoft 365 user account for Holly. You will also assign the Microsoft 365 Global Administrator role to Holly's account. This role will provide Holly with the permissions needed to perform all administrative functions within Microsoft 365. Following this task, you will log in using Holly's new account and you will perform all remaining labs using Holly's persona. 

**License Note:** Before creating Holly's account, you will first verify the number of available licenses. In doing so, you will note that while your lab tenant provides 20 Microsoft 365 E5 licenses and 20 Enterprise Mobility + Security E5 licenses, all those licenses have already been assigned to the existing user accounts created by your lab hosting provider. As such, you must first unassign one of each license from an existing user so that you can assign them to Holly.

**Important:** As a best practice in your real-world deployment, you should always write down the credentials of the first Global administrator account (in this lab, it's the MOD Administrator account, whose username is admin@xxxxxZZZZZZ.onmicrosoft.com, where xxxxxZZZZZZ is the tenant prefix assigned by your lab hosting provider). You should store away this account information for security reasons. **This account should be a NON-personalized identity** that owns the highest privileges possible in a tenant. It should **not** be MFA activated because it is not personalized. Because the username and password for this first Global admin account are typically shared among several users, this account is a perfect target for attacks; therefore, it's always recommended that organizations create personalized service admin accounts (for example, an Exchange admin, SharePoint admin, and so on) and keep as few personal Global admins as possible. For those personal Global admins that you do create in your real-world deployment, they should each be mapped to a single user (such as Holly Dickson), and they should each have Microsoft Entra Multi-Factor Authentication (MFA) enforced. That being said, Microsoft has already turned on MFA by default for all users in your Microsoft 365 trial tenant.

1. On the **LON-CL1** VM, the **Microsoft 365 admin center** should still be open in your Microsoft Edge browser from the prior lab exercise. You should be signed into Microsoft 365 as the **MOD Administrator**. 

2. Since you are adding a new user, you should begin by checking license availability before adding the user account. In the **Microsoft 365 admin center** navigation pane, select **Billing** to expand the Billing group, and then select **Licenses**. 

3. On the **Licenses** page, the **Subscriptions** tab is displayed by default. In the list of subscriptions, note the **Enterprise Mobility + Security E5** and **Microsoft 365 E5** subscriptions don't have any available licenses. Your lab tenant provides 20 licenses for each subscription, but all 40 licenses have been assigned. Since you must assign Holly both an **Enterprise Mobility + Security E5** license and a **Microsoft 365 E5** license, you must first unassign the licenses from an existing user account to make them available for Holly. 

4. In the **Microsoft 365 admin center** navigation pane, select **Users** and then select **Active users**. In the **Active users** list, you will see the list of existing user accounts that were created by your lab hosting provider. Since Christie Cline will be moving to a new role in the company and will no longer be part of the Microsoft 365 pilot project, you will unassign the **Enterprise Mobility + Security E5** and **Microsoft 365 E5** licenses from her account so that you can reassign them to Holly Dickson's new account.

5. On the **Active users** page, in the list of users, select **Christie Cline** (select Christie's hyperlinked name and not the check box next to her name).

6. In the **Christie Cline** pane that appears, the **Account** tab is displayed by default. Select the **Licenses and apps** tab. Under **Licenses (2)**, select the check boxes next to **Enterprise Mobility + Security E5** and **Microsoft 365 E5** to clear them, and then select **Save changes**. Once the changes are saved, close the **Christie Cline** pane.

7. You're now ready to create a user account for Holly Dickson, who is Adatum's new Microsoft 365 Administrator. In doing so, you will assign Holly the Microsoft 365 Global Administrator role, which gives Holly global access to most management features and data across Microsoft online services. You will also assign Holly the two licenses that you just unassigned from Christie Cline. <br/>

	In the **Active Users** window, select the **Add a user** option that appears on the menu bar above the list of active users. This starts the **Add a user** wizard.

8. In the **Set up the basics** page of the **Add a user** wizard, enter the following information:

	- First name: **Holly**

	- Last name: **Dickson** 

	- Display name: When you tab into this field, **Holly Dickson** will appear.

	- Username: **Holly** <br/>
	
		‎**IMPORTANT:** To the right of the **Username** field is the domain field. It will be prefilled with the **xxxxxZZZZZZ.onmicrosoft.com** cloud domain (where xxxxxZZZZZZ is the tenant prefix provided by your lab hosting provider).<br/>
	
	- Clear (uncheck) the **Automatically create a password** check box, which will display a new field for entering an administrator defined password.

	- In the new **Password** field that appears, enter the same **Administrative Password** provided by your lab hosting provider for the tenant admin account (i.e. the MOD Administrator account)

	- Clear (uncheck) the **Require this user to change their password when they first sign in** check box 

9. Select **Next**. If a **Save password** dialog box appears towards the top of the screen, select **Never**.

10. In the **Assign product licenses** page, enter the following information: <br/>

	- Select location: **United States**

	- Licenses: Under the **Assign user a product license** option, select the **Enterprise Mobility + Security E5** and **Microsoft 365 E5** check boxes

11. Select **Next**.

12. In the **Optional settings** page, select the drop-down arrow to the right of **Roles**. 

13. In the **Roles** section, select the **Admin center access** option. By selecting this option, the most commonly used Microsoft 365 administrator roles are enabled below it.  <br/>

	**Note:** All the admin roles will be displayed if you select **Show all by category**, which appears after the last common role. For Holly, you don't need to view all the admin roles by category, since Holly will be assigned the Global Administrator role that appears in the list of commonly used roles.

14. Select the **Global Administrator** check box. <br/>

	**Note:** A warning message will be displayed indicating that Adatum already has 7 Global admins. In a normal environment, this would be excessive and not recommended. For the purposes of this lab, the lab hosting provider assigned the Global admin role to the MOD Administrator and six other user accounts, which is not something you would normally see in a real-world deployment. However, for the purpose of this lab in your fictitious Adatum lab environment, ignore this message. **That being said, the best practice guideline that you should follow is to have from two to four Global Administrators in your real-world Microsoft 365 deployments.** 

15. Select **Next**.

16. On the **Review and finish** window, review your selections. If anything must be changed, select the appropriate **Edit** link and make the necessary changes. Otherwise, if everything is correct, select **Finish adding**. 

17. On the **Holly Dickson added to active users** page, under the **User details** section, select the **Show** option to verify Holly's password is the same **Administrative Password** provided by your lab hosting provider for the tenant admin account (i.e. the MOD Administrator account).  <br/>

	**Note:** If you accidentally entered a different password, then once you return to the **Active Users** page, you will need to select the **Reset a password** icon (the key icon that appears when you hover over Holly's account) to change her password to the correct value.

18. Select **Close.**

19. Remain logged into the Client 1 VM (LON-CL1) with the Microsoft 365 admin center open in your browser for the next task.

### Task 2 – Add Holly to the Microsoft 365 pilot project group

After completing the previous task, you should still be signed into the **Microsoft 365 admin center** as the **MOD Administrator** account. In this task, you will begin implementing Adatum’s Microsoft 365 pilot project as Holly Dickson, Adatum’s new Microsoft 365 Administrator. Therefore, you will begin this task by logging out of Microsoft 365 as the MOD Administrator and you will log back in as Holly. 

In a previous task, you created a Microsoft 365 group for the members of Adatum's pilot project team so that you could create a custom theme for that group. In this task, you will add Holly to this group. 

1. On the LON-CL1 VM, the **Microsoft 365 admin center** should still be open in your Microsoft Edge browser from the prior task. You should be signed into Microsoft 365 as the **MOD Administrator**. <br/>

	On the **Microsoft 365 admin center** tab, in the upper-right corner of the screen, note that it displays the MOD Administrator's name and a megaphone icon. The name is displayed because of the custom theme that you created in the prior lab exercise that was associated with a group of Microsoft 365 pilot project users that included the MOD Administrator. Keep this in mind once you log back in as Holly Dickson. <br/>

	Select the user icon for the **MOD Administrator** in the upper right corner of your browser. In the **MOD Administrator** window that appears, select **Sign out.** <br/>
	
	**Important:** When signing out of one user account and signing in as another, you should close all your browser tabs except for the **Sign out** tab. This is a best practice that helps to avoid any confusion by closing the windows associated with the prior user. Once you're signed out of the MOD Administrator account, take a moment and close all other browser tabs except for the **Sign out** tab. 
	
2. In your Microsoft Edge browser, in the **Sign out** tab, enter the following URL in the address bar to sign back into Microsoft 365: **https://portal.office.com**. 

3. In the **Pick an account** window, only the MOD Administrator's tenant admin account (the admin@xxxxxZZZZZZ.onmicrosoft.com account) that you just signed out from appears. Select **Use another account**. 

4. In the **Sign in** window, enter **Holly@xxxxxZZZZZZ.onmicrosoft.com** (where xxxxxZZZZZZ is the tenant prefix provided by your lab hosting provider). Select **Next**.

5. In the **Enter password** window, enter the same **Administrative Password** provided by your lab hosting provider for the tenant admin account (i.e. the MOD Administrator account) that you also assigned to Holly's account, and then select **Sign in**. If required, complete the MFA sign-in process.  <br/>

	**Note:** From this point forward, Holly and the MOD Admin will be the only users who are assigned the **Administrative Password** provided by your lab-hosting provider. All other users are assigned the **User Password** provided by your lab-hosting provider.

6. If a **Welcome to Microsoft 365** dialog box appears in the middle of the screen, there's no option to close it. Instead, to the right of the window, select the forward arrow icon (**>**) two times and then select the check mark icon to advance through the slides in this messaging window. 

7. If a **Create with Microsoft 365** window appears, select the **X** in the top corner of the window to close it. 

8. The **Welcome to Microsoft 365** page appears in your Edge browser in the **Home | Microsoft 365** tab. This is Holly's Microsoft 365 home page. Note that Holly's initials appear in the upper-right corner of the screen; however, Holly's name is not displayed. This is because Holly's account did not exist at the time you added the Microsoft 365 pilot project users to the group that was associated with the custom theme in the prior lab exercise. Since Holly wants to see her name at the top of each Microsoft 365 window when she's logged into the system, she first wants to add her account to the group of Microsoft 365 pilot project users. <br>

	In the column of application icons that appears in the navigation pane on the side of the screen, select **Admin**. This opens the **Microsoft 365 admin center** in a new browser tab. 

9. In the **Microsoft 365 admin center**, select **Teams & groups** in the navigation pane, and then under it, select **Active teams & groups**. 

10. In the **Active teams and groups** page, there's a tab for viewing each of the group types. The **Teams & Microsoft 365 groups** tab is displayed by default. In this tab, select **M365 pilot project**.

11. In the **M365 pilot project** pane that appears, the **General** tab is displayed by default. Select the **Membership** tab.

12. In the **Membership** tab, the **Owners** sub-tab is displayed by default in the navigation pane that appears on the side of the pane. Select the **Members** sub-tab that appears below it.

13. In the **Members** sub-tab, select **+Add members**.

14. In the **Add group members to M365 pilot project** pane that appears, select inside the **Search by name or email address** field. In the list of users that appears, scroll down and select **Holly Dickson**. Select the **Add (1)** button, and then close the **Add group members to M365 pilot project** pane once Holly is added to the group.

15. On the **Active teams and groups** page, select the **Refresh** icon that appears at the top of the screen, to the left of the address bar. Note how Holly Dickson's name appears next to her initials in the upper-right corner of the screen (Note: you may have to refresh twice to see Holly's name).

16. In the **Microsoft 365 admin center**, select **Users** in the navigation pane, and then under it, select **Active users**.

17. In the **Active Users** window, when you hover your mouse over a user's **Display name**, a **key icon** appears to the right of the user's name. By selecting the key icon, you can reset a user's password. You must reset the passwords for Adele Vance, Alex Wilber, Joni Sherman, Lynne Robbins, and Patti Fernandez to the same **Administrative Password** provided by your lab hosting provider for the tenant admin account (i.e. the MOD Administrator account) and that you previously assigned to Holly Dickson.<br/>

    Hover your mouse over **Adele Vance** and select the key icon that appears.

18. In the **Reset password** pane that appears for Adele, clear (uncheck) the **Automatically create password** check box. 

19. In the **Password** field that appears, enter the same **Administrative Password** provided by your lab hosting provider for the tenant admin account (i.e. the MOD Administrator account). Select the eye (**Show Password**) icon at the end of the **Password** field to display the value that you entered. Verify that you correctly entered the tenant password.

20. Clear (uncheck) the **Require this user to change their password when they first sign in** check box.

21. Select **Reset Password**. If a **Save password** dialog box appears at the top of the screen, select **Never**. Then select **Close** on the **Password has been reset** pane.

22. Repeat steps 17-21 for **Alex Wilber**, **Joni Sherman**, **Lynne Robbins**, and **Patti Fernandez**. Reset each of their passwords to the same **Administrative Password** provided by your lab hosting provider for the tenant admin account (i.e. the MOD Administrator account). In step 19, don't forget to show the password you entered to verify it's the correct value.

23. Remain logged into LON-CL1 with the **Microsoft 365 admin center** open in your browser for the next task.


### Task 3: Create a Conditional Access policy to implement MFA

**IMPORTANT:** This task begins by examining the Conditional Access policy that Microsoft created to implement MFA for all users. However, your Learning Partner may be using trial tenants that precede the recent MFA policy change. If you haven't been asked to perform MFA after each user sign-in, then your trial tenant doesn't require MFA. In this case, the MFA policy that Microsoft created won't appear in your policies list. If that's the case with your tenant, then you will skip the steps that review this policy. 

As your training indicated, there are three ways to implement MFA - with Conditional Access policies, with security defaults, and with legacy per-user MFA (not recommended for larger organizations). In this exercise, you'll enable MFA through a Conditional Access policy, which is the method that Microsoft recommends. Adatum has directed Holly to enable MFA for all its Microsoft 365 users - both internal and external. However, for the purpose of testing Adatum's Microsoft 365 pilot project implementation, Holly wants to exclude the members of the M365 pilot project group from having to use MFA to sign in. Once the pilot project is complete, Holly will update the policy by removing the exclusion of this group from the MFA requirement. The policy will also include two other requirements. It will require MFA for all cloud apps, and it will require MFA even if a user signs in from a trusted location. 

**Note:** While you will create a Conditional Access policy in this task that enables MFA, you will NOT enable it. Some students may have a tenant that requires MFA, in which case this policy will not be applied. And even if every student in your class has a tenant that doesn't require MFA, you will still not enable your policy. The point of this exercise is to provide you with experience on creating a policy to enable MFA and not actually authenticating with MFA, which we assume you know how to do. So we have chosen not to have students enable their policy, which provides the best compromise given the potential tenant situation in your class. 

1. On the LON-CL1 VM, the **Microsoft 365 admin center** should still be open in your Microsoft Edge browser from the prior task. You should be signed into Microsoft 365 as **Holly Dickson**.
   
2. In the **Microsoft 365 admin center**, under the **Admin centers** section in the navigation pane, select **Identity**. Doing so opens the Microsoft Entra admin center in a new browser tab. If a **Pick an account** window appears, select **Holly Dickson's account**.

3. In the **Microsoft Entra admin center**, select **Protection** in the navigation pane, and then select **Conditional Access**.

4. On the **Conditional Access | Overview** page, select **Policies** in the middle navigation pane.

5. On the **Conditional Access | Policies** page, review the default policies available with your Microsoft 365 subscription. Note the policy titled **Multifactor authentication for Microsoft partners and vendors**. This is the Conditional Access policy that Microsoft created that requires MFA for all users on all cloud apps. Select this policy so that you can see how Microsoft is enforcing MFA for all users in this trial tenant.   <br/>

	**IMPORTANT:** Your Learning Partner may be using trial tenants that precede this recent MFA change. If you haven't been asked to perform MFA after each user sign-in, then your trial tenant doesn't require MFA. In this case, the policy titled **Multifactor authentication for Microsoft partners and vendors** won't appear in your policies list, in which case you should skip to step 11 to begin creating your own Conditional Access policy. 

6. On the **Multifactor authentication for Microsoft partners and vendors** page, under the **Users** group, select **All users included and specific users excluded**. Doing so displays two tabs - **Include** and **Exclude**.

7. Under the **Include** tab, note that **All users** is selected. Just to satisfy your curiosity, let's try changing this policy by turning off MFA. Select **None** and then select the **Save** button. <br/>

	**Note what happened:** A message box briefly appeared at the top of the page indicating **Failed to update Multifactor authentication for Microsoft partners and vendors**. The system then returned you to the **Conditional Access | Policies** page. If you didn't see this message, then repeat this step again.  <br/>

	The same thing happens if, under the **Include** tab, you select **Users and groups** and you select specific users or groups rather than all users. In fact, Microsoft has built in a security firewall so that if you try to make any change to this policy, it will fail when you attempt to save the policy. 

8. Microsoft did build one exclusion into this policy. Let's take a look at it. On the **Policies** page, select the **Multifactor authentication for Microsoft partners and vendors** policy again, and then select **All users included and specific users excluded**. This time select the **Exclude** tab. 

9. Note that Microsoft selected the **Directory roles** checkbox. Select the field below this option. In the menu of roles that you can choose to exclude from MFA, the only role that Microsoft selected is **Directory Synchronization Accounts**. This role is automatically assigned to the Microsoft Entra Connect Sync service account and is not meant to be used otherwise. It's a special role that has permissions only to perform directory synchronization tasks. This role is crucial for synchronizing a local Active Directory Domain Services (AD DS) to Microsoft Entra ID, providing identity coexistence. Microsoft doesn't require MFA for this role because the synchronization service needs to run continuously without any interruptions that could be caused by MFA prompts. Additionally, this service account is configured with very limited permissions, and it isn't used for interactive sign-ins, which reduces the security risk.   <br/>

	As with the prior step where you tried to change the MFA setting to include no users or selected users, if you try to select other roles to get around the MFA setting, you will experience the same error indicating **Failed to update Multifactor authentication for Microsoft partners and vendors** when you try to save the policy. Microsoft's security firewall doesn't allow any change to this Conditional Access policy that affects those who must use MFA.

10. If you still have the **Multifactor authentication for Microsoft partners and vendors** page open, then select the **X** in the upper corner to close it and return back to the **Conditional Access | Policies** page. Or if you tried saving a change to the policy, your attempt will have failed, and you should already be back on the **Conditional Access | Policies** page.

11. On the **Conditional Access | Policies** page, on the menu bar at the top of the page, select **+New policy**.

12. On the **New Conditional Access policy** window, enter **MFA for all Microsoft 365 users** in the **Name** field.

13. You will begin by defining the MFA requirement for users. Under the **Users** group, select **0 users and groups selected**. Doing so displays two tabs - **Include** and **Exclude**.

14. Under the **Include** tab, select **All users**. Note the warning message that appears. You will address this in the next two steps.

15. Select the **Exclude** tab. To avoid system lockout, as the prior warning message indicated, you want to exclude your Global administrators - in this case, Holly. Holly also wants to exclude the other Microsoft 365 pilot project group members for the sake of expediency when testing. Once Microsoft 365 goes live, Holly will remove the pilot project group from the Exclude list in this Conditional Access policy and simply exclude herself and several other Global admins. But for now, Holly wants to exclude the entire group. <br/>

	To do so, select **Users and groups**. 

16. On the **Select excluded users and groups** window that appears, you want to select the Microsoft 365 pilot project group. The **All** tab is displayed by default. To quickly find the pilot project group, select the **Groups** tab. In the list of active groups, select the check box next to the **M365 pilot project** group, and then select the **Select** button at the bottom of the window. Back on the **New Conditional Access policy** window, note the message that appears under the **Users** section. 

17. You will now define the MFA requirement for all cloud apps. Under the **Target resources** section, select **No target resources selected**. Doing so displays two tabs - **Include** and **Exclude**.

18. Select the **Select what this policy applies to** drop-down field to see the various options in the drop-down menu. Select **Cloud apps**. 

19. Under the **Include** tab, note that the default setting is **None**. If you did not change this setting, then no cloud apps would require MFA - and that includes Microsoft 365. So even if you created this policy and selected the option to require MFA for all users, but you left this **Target resources** setting to **None**, then any user signing into Microsoft 365 would not have to use MFA. <br/>

	Under the **Include** tab, select the **Select apps** option. Doing so displays two sections - **Edit filter** and **Select**. Under the **Select** section, select **None**. In the **Select Cloud apps** pane that appears, scroll down through the list of apps to see all the different apps that you could require MFA for. **Do NOT select any of the apps.** We're having you scroll through this list just to get a feel for how granular you can get when requiring MFA should you decide to limit MFA to certain apps.  <br/>

	For Adatum, Holly wants to require MFA for all cloud apps, which is typically a more common business scenario than selecting specific apps. Under the **Include** tab, select the **All cloud apps** option. Adatum will not exclude any cloud apps from MFA authentication. You can select the **Exclude** tab if you want to see the options it provides. It works basically the same as the **Include** tab. You can view this tab, but do NOT select any cloud apps for exclusion. 

20. Finally, you will define the MFA requirement for all user sign-in locations. In some scenarios, organizations may only require MFA if a user signs-in from an untrusted location. However, Adatum wants to require MFA for all included users, regardless of where they sign in. <br/>

	Under **Conditions**, select **0 conditions selected**. Doing so displays a list of potential conditions the policy will check for. For this lab exercise, under the **Locations** condition, select **Not configured**. Doing so displays a **Configure** toggle switch and two tabs - **Include** and **Exclude**. Both tabs are currently disabled.

21. Set the **Configure** toggle switch to **Yes**, which enables the two tabs. 

22. Under the **Include** tab, verify **Any location** is selected (select it if necessary). Select the **Exclude** tab. If your organization recognizes specific IP addresses or ranges of addresses as "trusted", you can exclude the MFA requirement if a user signs in from one of those locations. However, Adatum wants to require MFA for all user sign-in attempts, regardless of their location. This will include both internal and external user sign-ins. Verify the **Selected locations** option is selected, and under the **Select** section, verify it says **None**. By not specifying any selected locations, this setting ensures that no locations are excluded from MFA. 

23. Under the **Access controls** section, under the **Grant** group, select **0 controls selected**. Doing so displays a **Grant** pane.

24. In the **Grant** pane that appears, verify the **Grant access** option is selected (select it if necessary). Then select the **Require multifactor authentication** check box. Note all the other access controls that are available that can be enabled with this policy. For this policy, you will only require MFA. Select the **Select** button at the bottom of the **Grant** pane, which closes the pane. 

25. **IMPORTANT:** At this point, you would normally set the **Enable policy** field to **On**. However, since some students may have older trial tenants that do not require MFA while others may have the new tenants that require it, you will NOT enable the policy that you just created. As such, set the **Enable policy** field to **Off**.

27. Select the **Create** button to create the policy.

28. On the **Conditional Access | Policies** window that appears, verify the **MFA for all Microsoft 365 users** policy appears and that its **State** is set to **Off**.

29. Remain logged into LON-CL1 with all your Microsoft Edge browser tabs open for the next task.

**Note:** As per the earlier discussion, there's no way to test your Conditional Access policy if you have a Microsoft 365 trial tenant that requires MFA. Microsoft's Conditional Access policy requires MFA for all users. When you have multiple policies requiring MFA, the most restrictive policy applies. In this case, Microsoft's policy is more restrictive than the one you just created that included exceptions for the pilot project group members, so there would be no way of testing your policy. If your tenant is an older one that doesn't require MFA, you will not test it since other students in your class may have tenants that already require them to use MFA. In lieu of having you test your policy while others can't, we have chosen not to test your policy. Even though you can't test your policy using this trial tenant, we encourage you to use this experience of creating a Conditional Access policy to require MFA in your real-world Microsoft 365 deployments.


### Task 4: Deploy Microsoft Entra Smart Lockout

Adatum’s CTO has asked you to deploy Microsoft Entra Smart Lockout, which assists in locking out bad actors who are trying to guess your users’ passwords or use brute-force methods to get admitted into your network. Smart Lockout can recognize sign-ins coming from valid users and treat them differently than sign-ins from attackers and other unknown sources. 

The CTO is anxious to implement Smart Lockout because it will lock out the attackers while letting Adatum’s users continue to access their accounts and be productive. The CTO has asked Holly to configure Smart Lockout so that users can’t use the same password more than once, and they can’t use passwords that are considered too simplistic or common. 

**Note:** You can maintain Account Lockout Policy settings in both the Group Policy Management Editor and in Microsoft Entra through its Smart Lockout feature. This lab task shows you how to access each method, although you will only update the Smart Lockout settings in Microsoft Entra. You must use the company's domain controller (LON-DC1) to access the Group Policy Management Editor. 

1. In the prior tasks, you worked in LON-CL1. In this task, you will be working from Adatum's domain controller, LON-DC1. <br/>

	Switch to **LON-DC1**.

2. On **LON-DC1**, you must select **Ctrl+Alt+Delete** to log in (your instructor will guide you on how to find this option in your VM environment). Log into LON-DC1 as the local Adatum administrator account that was created by your lab hosting provider (**Administrator**) with the password **Pa55w.rd**.

3. On LON-DC1, **Server Manager** automatically starts at boot-up. In **Server Manager**, select **Tools** in the upper-right menu bar, and in the drop-down menu, select **Group Policy Management.** Maximize the **Group Policy Management** window that appears.

4. You want to edit the group policy that includes your organization's account lockout policy. If necessary, in the root console tree in the side pane, expand **Forest:Adatum.com**, then expand **Domains**, and then expand **Adatum.com**.  <br/>

	‎Under **Adatum.com**, right-click on **Default Domain Policy** and then select **Edit** in the menu.

5. Maximize the **Group Policy Management Editor** window that appears.

6. In the **Default Domain Policy** tree in the side pane, under **Computer Configuration**, expand **Policies**, expand **Windows Settings**, expand **Security Settings**, and then expand **Account Policies.**

7. In the **Account Policies** folder, select **Account Lockout Policy**.

8. As you can see in the pane that appears, none of the smart lockout parameters have been defined. Instead of maintaining these lockout parameters in the Group Policy Management Editor, you're instead going to use the Microsoft Entra admin center. While you can use the Group Policy Management Editor, this method is typically used in on-premises Active Directory environments. We showed you this editor so that you could see this alternative. However, for organizations that strictly use cloud-based services like Microsoft 365, or who find using the Microsoft Entra admin center much more user-friendly than accessing the Group Policy Management Editor, using the **Microsoft Entra admin center** to assign corresponding values in the Entra ID context is preferrable. <br/>  

	Also keep in mind that the lockout behavior and customization options differ between the two methods. With the Group Policy Management Editor, you have more granular control over policy settings, including Account Lockout Threshold, Lockout Duration, and Reset Account Lockout Counter After. However, using this method requires familiarity with Group Policy and Active Directory administration. Conversely, the Account Lockout Policy in Microsoft Entra can't be customized as extensively. However, it’s easier to use, even though it lacks some of the fine-tuning options available in Group Policy. <br/>

	For Adatum, Holly has chosen to use the Microsoft Entra admin center to configure the company's Account Lockout policy. ‎On the taskbar at the bottom of your screen, select the **Microsoft Edge** icon. If necessary, maximize your browser window when it opens.

9. In your Edge browser, go to the **Microsoft 365 Home** page by entering the following URL in the address bar: **https://portal.office.com** 

10. In the **Sign in** dialog box, you must sign in as Holly Dickson. Enter **Holly@xxxxxZZZZZZ.onmicrosoft.com**, where xxxxxZZZZZZ is the tenant prefix assigned by your lab hosting provider. Select **Next**. <br/>

11. In the **Enter password** dialog box, enter the unique **Administrative Password** provided by your lab hosting provider and then select **Sign in**. If required, complete the MFA sign-in process.

12. On the **Stay signed in?** dialog box, select the **Don’t show this again** check box and then select **Yes.** On the **Save password** dialog box that appears, select **Never**.

13. If a **Welcome to Microsoft 365** dialog box appears in the middle of the screen, there's no option to close it. Instead, to the right of the window, select the forward arrow icon (**>**) two times and then select the check mark icon to advance through the slides in this messaging window. 

14. If a **Find more apps** window or a **Create with Microsoft 365** window appears, select the **X** in the upper top corner of the windows to close them. 

15. On the **Welcome to Microsoft 365** page, in the list of application icons that appear in the side window pane, select **Admin**; this opens the **Microsoft 365 admin center** in a new browser tab. 

16. In the **Microsoft 365 admin center**, select **Show all** in the navigation pane. Under **Admin centers**, select **Identity**, which displays the **Microsoft Entra admin center** in a new tab.

17. In the **Microsoft Entra admin center**, select **Protection** in the navigation pane, and then select **Authentication methods**.

18. In the **Authentication methods | Policies** page, in the middle pane under the **Manage** section, select **Password protection.**

19. In the **Authentication methods | Password protection** window, in the detail pane on the right, enter the following information:

	- In the **Custom smart lockout** section:

		- **Lockout threshold:** this field indicates how many failed sign-ins are allowed on an account before its first lockout. The default is 10. For testing purposes, Adatum has requested that you set this to **3**.

		- **Lockout duration in seconds:** This is the length in seconds of each lockout. The default is 60 seconds (one minute). Adatum has requested that you change this to **90** seconds.

	- In the **Custom banned passwords** section:

		- **Enforce custom list**: select **Yes**

		- **Custom banned password list:** Enter the following values (press Enter after entering each value so that each value is on a separate line):

			- **Password01**

			- **F00tball01**

			- **Se@Hawks1**

			- **Never4get!!**

	- In the **Mode** section, select **Enforced**

20. Select **Save** on the menu bar at the top of the page.

21. You should now test the banned password functionality. Select Holly Dickson's user icon in the upper right corner of the screen, and in the menu that appears select **View account**. 

22. In the **My account** window that appears, in the **Password** tile, select **CHANGE PASSWORD**.

23. A new tab will open displaying the **Change password** window. In the **Old password** field, enter Holly's existing password, which is the same **Administrative Password** provided by your lab hosting provider for the tenant admin account (i.e. the MOD Administrator account). <br/>

	Enter **Never4get!!** in the **Create new password** and **Confirm new password** fields, and then select **Submit**. Note the error message that you receive.

24. In your browser, close the **Change password** tab. 

25. You should now test the lockout threshold functionality. Select Holly Dickson's user icon in the upper right corner of the screen, and in the menu that appears select **Sign out**.  

26. Once you are signed out as Holly, the **Pick an account** window will appear in the **Sign in to Microsoft Entra** tab. As a best practice when signing out from a Microsoft online service as one user and signing back in as another, close all your browser tabs except for the **Sign out** or **Sign in** tab. In this case, close the other tabs now and leave the **Sign in** tab open.  <br/>

	In the **Pick an account** window, select **Use another account**. 

27. In the **Sign in** window, you're going to sign in as Patti Fernandez. Enter **pattif@xxxxxZZZZZZ.onmicrosoft.com** (where xxxxxZZZZZZ is the tenant prefix assigned to you by your lab hosting provider), and then select **Next**. 

28. On the **Enter password** window, enter any random mix of letters and numbers and then select **Sign in**. Note the invalid password error message that appears. 

	Repeat this step 2 more times. 
	
	Since you set the **Lockout threshold** to **3**, you should receive an error message indicating that this account is locked after the third failed sign-in attempt. <br/>

	**Note:** If you do not receive this lockout message after the third attempt, then the system has not yet finished propagating this lockout threshold change throughout the service. It may take several minutes for the change to take effect. Wait a few minutes and then sign-in again with a bogus password. Testing of this lab has seen varying results. The change sometimes propagates almost immediately so that you get locked out after the third sign-in attempt. Other times it has taken anywhere from 5 to 10 minutes before the lockout message is displayed. Continue this process until you receive the lockout message, at which point Patti's account will be temporarily locked to prevent unauthorized access.

29. You will be prohibited from logging in again as Patti until after the **90 second lockout duration** that you set earlier. <br/>

	Once you've been locked out, wait 90 seconds and then sign back in as **pattif@xxxxxZZZZZZ.onmicrosoft.com** (where xxxxxZZZZZZ is the tenant prefix assigned to you by your lab hosting provider). In the **Password** field, enter Patti's password, which is the **User Password** provided by your lab hosting provider. If required, complete the MFA sign-in process. Verify that you are able to successfully sign-in as Patti.

30. Once your log-in is successful, you can close all open applications. This will be your last lab exercise using the LON-DC1 domain controller.
 
# Proceed to Lab 2 - Exercise 2
