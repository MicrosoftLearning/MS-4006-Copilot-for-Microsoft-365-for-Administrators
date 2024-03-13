# Learning Path 3 - Lab 3 - Exercise 1 - Implement Sensitivity labels with Microsoft Entra ID Protection

In your role as Holly Dickson, Adatum’s new Microsoft 365 Administrator, you have Microsoft 365 deployed in a virtualized lab environment. As you proceed with your Microsoft 365 pilot project, your next steps are to implement Sensitivity Labels with Microsoft Entra ID Protection at Adatum. In this lab, you will create and publish a label, and you will test a published label. However, in doing so, you won't test the label that you create in this lab. Instead, you will test a different label.

**Important:** When you publish a new sensitivity label and label policy, it can take them up to 24 hours to propagate through Microsoft 365. As such, you won't be able to test the label that you create in this lab. Instead, you will test a pre-existing sensitivity label named **Project - Falcon**. This pre-existing label is almost identical to the label that you will create, so you'll be able to see the same results had you been able to test the label that you created. 


### Task 1 – Install the Microsoft Entra ID Protection Unified Labeling client

To implement Sensitivity labels as part of your pilot project at Adatum, you must first install the Microsoft Entra ID Protection client from the Microsoft Download Center.

**Note:** While the Azure AD to Microsoft Entra ID rebranding is still ongoing, the Azure Information Protection client has not been rebranded as of this writing. It will eventually be rebranded to Microsoft Entra ID Protection client.

1. At the end of the prior lab, you were on LON-CL2. Switch to **LON-CL1**.  <br/>

	You should still be logged into LON-CL1 as the local **adatum\administrator** account, and in your Edge browser, you should still be logged into Microsoft 365 as **Holly Dickson**. 

2. In **Microsoft Edge**, open a new tab and enter (or copy and paste) the following URL in the address bar: **https://www.microsoft.com/en-us/download/confirmation.aspx?id=53018** <br/>

	This will start the download for the Azure Information Protection Unified Label client.

3. In the **Downloads** window that appears at the top right of the page, you will see the **AzInfoProtection_UI.exe** file being downloaded. Once the file has finished downloading, select the **Open file** link that appears below the file name.

4. The **Microsoft Azure Information Protection** wizard will open. If the wizard does not display on the desktop, select the icon for the wizard on the taskbar to display the wizard.

5. In the wizard, on the **Install the Azure Information Protection client** window that appears, clear (uncheck) the **Help improve Azure Information Protection by send usage statistics to Microsoft** check box and then select the **I agree** button.

6. If a **User Account Control notification** dialog box appears that asks whether the app is allowed to make changes to this device, select **Yes**.

7. Once the installation is complete, select **Close**.

8. In your Edge browser, close the **Download** tab that you opened in this task to download the Azure Information Protection client.

You have successfully installed the Azure Information Protection Unified Label client on the LON-CL1 VM.


### Task 2 – Create a Sensitivity Label

In this exercise you will create a Sensitivity Label and add it to the default policy so that it’s valid for all users of the Adatum tenant.

1. On LON-CL1, in your Edge browser, you should still be logged into Microsoft 365 as **Holly Dickson**.

2. In your Edge browser, you should still have a tab open for the **Microsoft 365 admin center**. If not, open a new tab and enter the following URL: **https://admin.microsoft.com**.

3. On the **Microsoft 365 admin center**, if necessary, select **... Show all** in the navigation pane. Select **Compliance** under the **Admin centers** group.

4. On the **Microsoft Purview** compliance portal, select **Information protection** in the navigation pane and then select **Labels**. 

5. On the **Labels** page, a warning message is displayed in a light yellow shaded box in the middle of the page indicating: **Your organization has not turned on the ability to process content in Office online files that have encrypted sensitivity labels applied and are stored in OneDrive and SharePoint. You can turn on here, but note that additional configuration is required for Multi-Geo environments.** <br/>

    Select the **Turn on now** button that appears on the right side of this message. This will enable Adatum to apply the Sensitivity labels inside its Microsoft 365 environment. <br/>

    Note how the message has now changed to indicate: **You can now create sensitivity labels with privacy and access control settings for Teams, SharePoint sites, and Microsoft 365 Groups.**	

6. On the **Labels** page, select the **+Create a label** option that appears on the menu bar in the middle of the screen, below the previous message. This initiates the **New sensitivity label** wizard.

7. In the **New sensitivity label** wizard, on the **Provide basic details for this label** page, enter the following information:

	- Name: **PII**
	
	- Display name: **PII**

	- Description for users: **Documents, files, and emails with PII**

	- Description for admins: **Documents, files, and emails with PII**

	- Label color: select one of the colors that you want to assign to your sensitivity labels

8. Select **Next**.

9. On the **Define the scope for this label** page, verify the **Items** check box is selected (select it now if necessary) and then select **Next**.

10. On the **Choose protection settings for labeled items** page, select both check boxes for **Apply or remove encryption** and **Apply content marking**, and then select **Next**.

11. On the **Encryption** page, you will define who can access items that have this label applied. Select the **Remove encryption if the file or email or calendar event is encrypted** option and then select **Next**.

12. On the **Content marking** page, set the **Content marking** toggle switch to **On**. This displays three options that enable you to customize how you want to mark files and emails. <br/>

	Select all three check boxes. Under each setting, select **Customize text**. This opens a pane to customize that particular setting. Enter the following information in the **Customize** pane for each option (select **Save** after entering the settings for each option): <br/>

	- **Add a watermark** 
		- Watermark text: **Sensitive - Do Not Share** (Hint: after entering this value, copy it (Ctrl+C) so that you can paste it (Ctrl+V) in the other two text settings)
		- Font size: **25**
		- Font color: **Blue**
		- Text layout: **Diagonal**
			
	- **Add a header** 
		- Header text: **Sensitive - Do Not Share**
		- font size: **25**
		- Font color: **Red**
		- Align text: **Center**
			
	- **Add a footer**
		- Footer text: **Sensitive - Do Not Share**
		- font size: **25**
		- Font color: **Red**
		- Align text: **Center**

13. On the **Content marking** page, select **Next**. 

14. On the **Auto-labeling for files and emails** page, set the **Auto-labeling for files and emails** toggle switch to **On**. This enables a series of options that you will update in the next steps.

15. Under **Detect content that matches these conditions**, select **+Add condition** and then select **Content contains**.

16. In the **Content contains** window, select the **Add** drop-down arrow and then select **Sensitive info types**.

17. In the **Sensitive info types** window, hover your mouse to the left of the **Name** column heading. Select the check box that appears, which automatically selects all the sensitive information types. Select **Add**, which will add all these sensitive information types to your label.

18. On the **Auto-labeling for files and emails** page, all of the sensitive information types that you selected will be displayed. Scroll to the bottom on the window and update the following settings:

	- When content matches these conditions: select **Automatically apply the Label**

	- Display this message to users when the label is applied: enter **Sensitive content has been detected and will be encrypted**.
		
19. Select **Next**.

20. On the **Define protection settings for groups and sites** page, leave both check boxes blank and select **Next**.

21. On the **Auto-labeling for schematized data assets (preview)** page, do not enable Auto-labeling for schematized data assets (preview). Select **Next**. 

22. On the **Review your settings and finish** page, review the information you entered. If any settings need to be corrected, select the corresponding **Edit** option and make any necessary changes. When all information appears correct, select **Create label**.

23. A **Client Error** dialog box should appear that states the generated rule blob for the label you are attempting to create is too long. The maximum size of sensitive information type selections you can make at one time per rule is **49152**. By selecting all the sensitive information types like you did in the **Sensitive info types** window a few steps back, you have exceeded this limit. <br/>

	**NOTE: We purposely had you select all the sensitive information types so that you would receive this error.** We wanted you to experience this error so that if it happens in your production environments, you will know why you received the error and how you can correct it.  <br/>

	To correct this issue, select **OK** in the **Client Error** dialog box, and then on the **Review your settings and finish** page, scroll down to the **Auto-labeling for files and emails** section and select **Edit**.
	
24. This should return you to the **Choose protection settings for labeled items** page in the wizard. Select **Next** on this page, select **Next** on the **Encryption** page, and then select **Next** on the **Content Marking** page. This will take you to the **Auto-labeling for files and emails** page. 

25. On the **Auto-labeling for files and emails** page, to the right of the **Content contains** condition, select the **trash can icon**. This will remove the existing **Content contains** condition for the **PII** label that you created. <br/>

	In the remaining steps, you will add a new condition that only contains two sensitivity information types rather than all the sensitivity information types like you did originally.

26. On the **Auto-labeling for files and emails** page, under **Detect content that matches these conditions**, select **+Add condition** and then select **Content contains**.

27. In the **Content contains** window, select the **Add** drop-down arrow and then select **Sensitive info types**.

28. In the **Sensitive info types** window, in the list of sensitive information types, only select the **ABA routing number** and the **U.S. Social security Number (SSN)** check boxes, and then select **Add**. Back on the **Auto-labeling for files and emails** page, both of these sensitive information types will appear. Select **Next**.

29. On the **Define protection settings for groups and sites** page, leave the two check boxes blank and select **Next**.

30. On the **Auto-labeling for schematized data assets (preview)** page, do not enable Auto-labeling for database columns. Select **Next**.

31. On the **Review your settings and finish** page, select **Create label**.

32. On the **Your sensitivity label was created** page, select the **Don't create a policy yet** option and then select **Done**. This returns you to the **Labels** page.

33. Now it's time to publish the **PII** label. On the **Labels** page, if the **PII** label does not appear in the list of labels, select **Refresh** on the menu bar. Once the **PII** label appears, select the check box that appears to the left of it. 

34. Select the **Publish label** option that appears in the menu bar above the list of labels. This initiates a **Create policy** wizard.

35. In the **Create policy** wizard, on the **Choose sensitivity labels to publish** page, the **PII** label is already listed, so select **Next**. 

36. On the **Assign admin units** page, select **Next** since you'll be assigning this PII policy to Adatum's full directory rather than just a select group of admin units.

37. On the **Publish to users and groups** page, you can choose whether to make your policy available to all users and groups, or you can limit the policy to selected users and groups. For this lab, you want to make the policy available to everyone. The **Users and groups** option is already selected by default (if not, then select it now). This will make your policy available to all users and groups. Select **Next**.  <br/>

	**Note:** When doing this in your real-world deployment, if you want to limit your policy to a select number of users or groups, then you would select **Edit** and make those selections. 

38. On the **Policy settings** page, select the **Users must provide a justification to remove a label or lower its classification** check box, and then select **Next**. 

39. On the **Apply a default label to documents** page, select **PII** in the drop-down menu that appears, and then select **Next**.

40. On the **Apply a default label to emails** page, select **PII** in the drop-down menu that appears, and then select **Next**.

41. On the **Apply a default label to meetings and calendar events** page, select **PII** in the drop-down menu that appears, and then select **Next**.

42. On the **Apply a default label to Fabric and Power BI content** page, select **PII** in the drop-down menu that appears, and then select **Next**.

43. On the **Name your policy** page, enter **PII Policy** in the **Name** field, and then enter (or copy and paste) the following description for this sensitivity label policy: **The purpose of this policy is to detect sensitive information such as ABA bank routing numbers and US social security numbers in emails and documents, and to encrypt this information when it's discovered. The user must provide an explanation for removing the classification label.** Select **Next**.

44. On the **Review and finish** page, review the information you entered. If anything needs to be corrected, select the corresponding **Edit** option and make the necessary corrections. When all information is correct, select **Submit**.

45. On the **New policy created** page, select **Done**.


### Task 3 – Assign a pre-existing sensitivity label to a document

As outlined in the instructions at the start of this lab, it isn't possible to immediately test the sensitivity label and label policy that you created in the previous task. This is because it takes up to 24 hours for a new label policy to propagate through Microsoft 365 and for its label to become visible in applications like Microsoft Word and Outlook.

Instead, you will test one of Microsoft 365's pre-existing sensitivity labels. For this lab, you will use the **Project - Falcon** sensitivity label, which is a Highly Confidential label. In fact, this label is similar to the label that you created in the prior task - the one exception being that it doesn't include a header or footer. Using this pre-exsiting label will give you a good idea as to how the label that you created would work at Adatum.

1. On LON-CL1, in your Edge browser, you should still be logged into Microsoft 365 as **Holly Dickson**.

2. To validate the **Project-Falcon** sensitivity label, you must first sign out of Microsoft 365 as Holly and sign back in as **Alex Wilber**. <br/>

	In your Edge browser, select the **Microsoft 365 admin center** tab, and then select the circle with Holly Dickson's HD initials in the upper right corner of the screen. In the **Holly Dickson** window, select **Sign out**.

3. Once you are signed out, close all the tabs in your Edge browser except for the **Sign out** tab.

4. In the **Sign out** tab, enter the following URL in the address bar: **https://portal.office.com/** 

5. In the **Pick an account** window, select **Use another account**.

6. In the **Sign in** window, enter **AlexW@xxxxxZZZZZZ.onmicrosoft.com** (where xxxxxZZZZZZ is the tenant prefix provided by your lab hosting provider) and then select **Next**.

7. On the **Enter password** window, enter the same **Administrative Password** provided by your lab hosting provider for the tenant admin account (i.e. the MOD Administrator account) and then select **Sign in**.

8. If a **Welcome to Microsoft 365** window appears, select the **forward arrow (>)** twice and then the check mark to close it. If a **Get your work done with Office 365** window appears, or a **Create with Microsoft 365** window, select the **X** to close them. 

9. On the **Welcome to Microsoft 365** home page, in the column of app icons on the left-side of the screen, right-click on the **Word** icon and select **Open in new tab**. This will open a new tab titled **Word | Microsoft 365**.

10. In the **Word | Microsoft 365** tab, under the **Create new** section at the top of the page, select **Blank document**.

11. If a **Your privacy option** window appears, select **Close**.

12. If the Word ribbon displays icons for each feature but does not break the icons out by group, then select the down-arrow on the far right-side of the ribbon, and then under **Ribbon layout**, select **Classic ribbon**. This will switch the ribbon to the traditional ribbon style that is broken out by feature group (such as Undo, Clipboard, Font, Paragraph, Styles, and so forth).

13. In the **Word** document, type **Testing a sensitivity label on a document with personally identifiable information (PII).**

14. Because you enabled Sensitivity labels at the start of this exercise, Word should display a **Sensitivity** group on the ribbon at the top of the page. Select the down arrow in the **Sensitivity** group. In the drop-down menu that appears, it should display the list of sensitivity label types. Select **Highly Confidential**, and then in the sub-menu that appears, select **Project - Falcon**. <br/>

	**Note:** After 24 hours, the label that you created in the prior task will appear in the Highly Confidential sub-manu, next to the Project-Falcon label. 

15. In the document, note how the sensitivity label applied a **CONFIDENTIAL - ProjectFalcon** watermark across the top of the document. </br>

	**Note:** This watermark is displayed at the top of the document while you're editing the document. This is not the official watermark that appears when the document is viewed in "Reading View" (i.e. as it would appear to a person reading the document). You will test how this watermark appears in Reading View in a later step. 	

16. In this first validation test, you're going to remove this sensitivity label from being applied to this document. One of the label policy options requires users to provide justification to remove a label or to select a lower classification label. You will now verify whether this setting is functioning properly. <br/>

	In the **Sensitivity** group in the Word ribbon, select the down arrow. In the drop-down menu that appears, note that a check mark appears next to **Highly Confidential**. Hold your mouse over **Highly Confidential** to display the sub-menu. Notice how a check mark appears next to **Project - Falcon**. The check marks identify the current label being applied to the document.  <br/>
 
	To remove the label from this document, select the **Project - Falcon** label that appears in this drop-down menu.
	
17. In the **Justification Required** window that appears, select the **Other (explain)** option. In the **Explain why you're changing this label** field, enter **Testing what happens when a label is removed from a document** and then select **Change**.

18. Note how the watermark in the document has disappeared. In the **Sensitivity** group in the Word ribbon, select the down arrow. In the drop-down menu that appears, note that while **Highly Confidential** > **Project - Falcon** is displayed, no check marks appear next to them. This indicates the sensitivity label is no longer being applied to this document.  

19. To re-apply the sensitivity label to the document, select **Highly Confidential** > **Project - Falcon** in the drop-down menu. Note how the watermark reappears in the document.

20. In the Word document, enter **111-11-1111** below the previous line of text that you entered. This number is the same format as a U.S. Social Security Number. <br/>

	**Note**: In Word for the Web, the custom watermark specificed in the **Project - Falcon** policy does not display by default. To view the custom watermark, select the **View** tab and then in the Word ribbon, select **Reading View**. Note how the watermark appears diagonally across the middle of the document. This is how the watermark will appear to someone reading the document. Alternatively, in the real world, you could use the Word Desktop App which would display the watermark in this format by default. <br/>

	To exit Reading View, select the **Edit Document** drop-down menu and then select **Edit**.

21. You will now save the document. On the title bar, to the right of Word, select **Document** (or **Document1**, whichever default name Word applies to the document). In the drop-down menu that appears, confirm the file **Location** says **Alex Wilber > Documents**. <br/>

	In the **File Name** field, rename the file to **ProtectedDocument1** and then select outside of this file name menu (select inside the document). Note the new name assigned to the file appears in the title bar. 

22. At the top-right side of the page, below Alex Wilber's name and picture, select the **Share** button. In the drop-down menu that appears, select **Share**.

23. In the **Share "ProtectedDocument1"** window that appears, select the **Gear icon** (Link settings) next to the **Copy link** button. 

24. On the **Link settings** window that appears, select **People you choose**. <br/>
	
	Under **More settings**, the current option is **Can edit**. You plan to share this document with Joni Sherman, but you only want Joni to be able to view the document. To make this permissions change, select **Can edit**. In the menu that appears, you can see that **Can edit** has a check mark next to it, which indicates this is the current setting. To limit Joni to read-only permission, select **Can view** and then select **Apply**.

25. Back on the **Share "ProtectedDocument1"** window, enter **Joni** in the **Add a name, group, or email** Field. A list of users whose name starts with **joni** should appear. Select **Joni Sherman**.

26. On the **Share "ProtectedDocument1"** window, hover your mouse over the "eye" icon that appears to the right of Joni's name. Doing so should display **Can view**, which is the current setting that you assigned to her for this document. The "eye" icon is the designation for "Can view". Select the **Copy link** button. 

27. Once the **Link copied** message appears at the bottom of the **Share "ProtectedDocument1"** window, then select the X in the upper-right corner of the window to close it.

28. Leave the **ProtectedDocument1** tab open displaying the document. You may need to reference this document in the next exercise if you need to recopy its link.

You have just successfully created a Word document that is read-only protected using Microsoft Entra ID Protection. The document is accessible only by its creator, Alex Wilber, and by Joni Sherman (with Read-only permission), to whom the document was shared.

### Task 4 – Verify the pre-existing sensitivity label policy

In the prior task, you created a Word document and protected it with the **Project - Falcon** sensitivity label. This label inserted a watermark in the document, and you restricted permissions on the document to Joni Sherman. To verify whether the protection that you assigned to the document works, you will first email the document to two persons - to Joni Sherman and to your own personal email address. Note that you will send a second email to Joni that includes a link to the document that allows Joni to edit it. The purpose of the two emails, one with document link that provides read-only access and another with a document link that provides the ability to edit the document, is to allow you to see how the functionality differs depending on the permissions assigned to the link. You will then test what functionality is possible for Joni Sherman, Alex Wilber, and yourself. 

1. On LON-CL1, in your Edge browser, you should still be logged into Microsoft 365 as **Alex Wilber** from the prior task with the **Word** tab open. 

2. In your Edge browser, select the **Home | Microsoft 365** tab. Doing so returns to the **Welcome to Microsoft 365** home page.

3. In the **Welcome to Microsoft 365** page, select the **Outlook** icon in the column of app icons on the left-side of the screen. This opens Alex Wilber's mailbox in Outlook on the web in a new browser tab. 

4. In **Outlook on the Web**, select **New Mail** in the upper left part of the screen.

5. In the right-hand pane, enter the following information in the email form:

	- To: Enter **Joni** and then select **Joni Sherman** from the user list. 

	- CC: Enter your own personal email address (do NOT enter Holly's email address; instead, enter your own personal email address), and then select the **Use this address: <your email address>** message that appears

	- Add a subject: **Protected Document Test - View only permission**

	- Body of the message: enter **If you can open the protected and restricted document attached to this email, then try to change it.**

6. In the body of the message, under the text you added in the previous step, paste the link copied to your clipboard from the prior task. A link for the file named **ProtectedDocument1.docx** should appear. <br/>

	**Note**: If the copied link from the prior exercise is no longer in your clipboard, you will need to re-copy the link. To do so, perform the following steps: <br/>

	- Select the **ProtectedDocument1** tab in your browser and then on the right-side of the menu bar select the **Share** button. In the drop-down menu that appears, select **Share**. 
	- In the **Share "ProtectedDocument1"** window, enter **Joni** in the **Add a name, group, or email** field and then select **Joni Sherman**. 
	- At the bottom of the window, select the **Gear icon** (Link settings) next to the **Copy link** button. 
	- On the **Link settings** window that appears, select the **People you choose** option. 
	- Under **More settings**, select **Can edit**. In the menu that appears, select **Can view** and then select **Apply**.
	- In the **Share "ProtectedDocument1"** window, select the **Copy link** button.
	- Select the **Mail - Alex Wilber - Outlook** tab in your browser and then paste the link into the body of the email message. 

7. Select **Send**.

8. A **Recipients can't access links** message should appear. This is due to the fact that you CC'd your personal email address in the email, but you don't have permission to access the document. Let's continue testing the permissions, so select **Send anyway**.

9. Select **Send**.

10. Switch to **LON-CL2**. 

11. On **LON-CL2**, you should be logged into **Outlook on the Web** as **Lynne Robbins** from the previous lab exercise. Sign out as Lynne.

12. In your Edge browser, close all tabs except for the **Sign out** tab. In this tab, enter the following URL in the address bar: **https://outlook.office365.com** 

13. In the **Pick an account** window, select **Use another account**.

14. In the **Sign in** window, enter **JoniS@xxxxxZZZZZZ.onmicrosoft** (where xxxxxZZZZZZ is the tenant prefix provided by your lab hosting provider) and then select **Next**.

15. On the **Enter password** window, enter the same **Administrative Password** provided by your lab hosting provider for the tenant admin account (i.e. the MOD Administrator account) and then select **Sign in**.

16. If a **Welcome** window appears, select the X to close it.

17. In Joni’s **Inbox** in **Outlook on the Web**, you should see the email that Alex sent whose Subject line indicates the document has View only permission. Open this email.

18. In the email, select the attached file to open it.

19. In the **Your privacy option** dialog box that appears, select **Close**. The document opens in **Word on the Web** in a new browser tab titled **ProtectedDocument1** tab. Note how the document appears in the Reading View in **Word on the Web**. This is Joni's indication that she has View only permission and can't edit the document. Review the document, noting the watermark specificed in the **Project - Falcon** policy. <br/>

	Once you have finished reviewing the document, close the **ProtectedDocument1** tab. 

20. You will now test what happens when you attempt to open the document that was sent to your personal email address. Use your phone or classroom PC to access your personal email address. Open the email that Alex just sent to your personal email address, and then attempt to open the attached file. 

21. Since you don't have permission to access to the document, a **Pick an account** window should appear. In a real-world scenario, you could optionally sign in with an account that has permission to access the file, or request access from the **AlexW@xxxxxZZZZZZ.onmicrosoft.com** account. <br/>

	At this point, you verified that you can't access the file because it was only shared with Joni Sherman. You also verified that Joni was only able to view the file, but not edit it. You will now change the Share permissions on the file by allowing Joni to edit it. You will do so to see how this experience differs from the one you just completed. 

22. Switch to **LON-CL1**. 

23. On LON-CL1, in your Edge browser, you should still be logged into Microsoft 365 as **Alex Wilber**, and you should have tabs open for both **Word** and **Outlook**. Select the **Mail - Alex Wilber - Outlook** tab. 

24. In Alex's mailbox, create another email to Joni Sherman. Do NOT include your personal email address in the CC line. Enter the following information in the email form:

	- To: Enter **Joni** and then select **Joni Sherman** from the user list. 

	- CC: leave blank

	- Add a subject: **Protected Document Test - Edit permission**

	- Body of the message: enter **If you can open the protected and restricted document attached to this email, then try to change it.**

25. Before you copy in the link to the document, you should change the permission by sharing it to Joni, but this time with Edit permission. To do so, perform the following steps: <br/>

	- Select the **ProtectedDocument1** tab in your browser and then on the right-side of the menu bar select the **Share** button. In the drop-down menu that appears, select **Share**. 
	- In the **Share "ProtectedDocument1"** window, enter **Joni** in the **Add a name, group, or email** field and then select **Joni Sherman**. 
	- At the bottom of the window, select the **Gear icon** (Link settings) next to the **Copy link** button. 
	- On the **Link settings** window that appears, select the **People you choose** option. 
	- Under **More settings**, if **Can edit** appears, then select **Apply**. However, if **Can view** appears, then select **Can view**, and in the menu that appears, select **Can edit** and then select **Apply**.
	- In the **Share "ProtectedDocument1"** window, select the **Copy link** button.
	- Select the **Mail - Alex Wilber - Outlook** tab in your browser and then paste the link into the body of the email message. 

26. Select **Send**.

27. Switch to **LON-CL2**. 

28. On **LON-CL2**, you should still be logged into **Outlook on the Web** as **Joni Sherman**. In Joni’s **Inbox**, you should see the email that Alex just sent whose Subject line indicates the document has Edit permission. Open this email.

29. In the email, select the attached file to open it.

30. When Joni had View only permission, the document opened in the Reading View pane. As such, Joni could not edit the document. This version of the document provides Joni with Edit permission, so this time the document should open in Word in normal edit mode. Verify that you can enter something into the document. 

	**Note:**  In this task, you just verified that Microsoft Entra ID Protection protected the document based on the PII policy parameters that you configured. When Joni was assigned View only permission, the document opened in the Reading view and she was unable to change it. When Joni was assigned Edit permission, the document opened in Word and she was able to change it. And since Alex didn't share the document with you, you couldn't open it when Alex sent the document in an email to your personal mailbox. 


## Congratulations! You have just completed the final lab in this course.
