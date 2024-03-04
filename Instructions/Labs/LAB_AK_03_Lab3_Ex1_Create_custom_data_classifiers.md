# Learning Path 3- Lab 3 - Exercise 1 - Create custom data classifiers

In this lab exercise, you will create a custom data classifier, a custom trainable classifier, and a document fingerprint classifier, and use them to apply labels and actions to data in your organization.

### Task 1 – Create a custom data classifier

In this task, you will create a custom data classifier that applies the label "Sensitive" to data that contains the word "secret". You will configure the data classifier to encrypt the data and add a watermark that says "Sensitive".

1. On LON-CL1, in your Edge browser, you should still be logged into Microsoft 365 as **Holly Dickson**.

2. In your Edge browser, select the **Microsoft 365 admin center** tab. In the left-hand navigation pane, under **Admin centers**, select **Security**. This will open a new tab in your browser for **Microsoft Defender**. 

Create a custom data classifier:
1.	Sign in to the Microsoft 365 Compliance Center with your admin credentials.
2.	On the left navigation pane, click on "Data classification".
3.	On the data classification page, click on the "Sensitivity labels" tab.
4.	Click on the "+ Create a label" button on the top right corner of the page.
5.	On the create a label page, specify the name as "Sensitive", description as "Data that contains the word 'secret'", tooltip as "Sensitive data", and choose a color for the data classifier.
6.	Configure the protection settings by selecting the "Encrypt" option and adding a watermark that says "Sensitive".
7.	Click on the "Next" button to proceed to the next step.
8.	Define the scope and settings of the data classifier by choosing whether it applies to files, emails, or both, and whether it is mandatory or recommended for users.
9.	Click on the "Next" button to proceed to the next step.
10.	Review and publish the data classifier by choosing whether to apply it to existing or new content, and whether to enable auto-labeling for the data classifier.
11.	Click on the "Publish" button to finalize and publish the data classifier.

    
### Task 2 – Create a custom trainable classifier

In this task, you will create a custom trainable classifier that identifies documents that contain resume information from job applicants. Your tenant includes several ficitious resumes that will be used to train the model. Configure the trainable classifier to apply the label "Resume" to the documents and delete them after 30 days.

1. On LON-CL1, in your Edge browser, you should still be logged into Microsoft 365 as **Holly Dickson**.

2. In your Edge browser, select the **Microsoft 365 admin center** tab. In the left-hand navigation pane, under **Admin centers**, select **Security**. This will open a new tab in your browser for **Microsoft Defender**. 



Create a custom trainable classifier:
1.	Sign in to the Microsoft 365 Compliance Center with your admin credentials.
2.	On the left navigation pane, click on "Data classification".
3.	On the data classification page, click on the "Trainable classifiers" tab.
4.	Click on the "+ Create classifier" button on the top right corner of the page.
5.	On the create classifier page, specify the name as "Resume" and description as "Documents that contain resume information".
6.	Choose to use a custom model and provide a set of seed data that contains examples of the data that you want to classify.
7.	Upload the seed data from your local device or from a SharePoint site.
8.	Specify the confidence level and the minimum number of matches for the model to apply a label or an action.
9.	Click on the "Next" button to proceed to the next step.
10.	Review and test the trainable classifier and choose whether to enable auto-labeling for the trainable classifier.
11.	Click on the "Create" button to finalize and create the trainable classifier.

### Task 3 – Create a document fingerprint classifier

In this task, you will create a document fingerprint classifier that detects documents that contain health records based on the template or the sample document that you have. You will configure the document fingerprint classifier to apply the label "Health Record" to the documents and notify the admin.

1. On LON-CL1, in your Edge browser, you should still be logged into Microsoft 365 as **Holly Dickson**.

2. In your Edge browser, select the **Microsoft 365 admin center** tab. In the left-hand navigation pane, under **Admin centers**, select **Security**. This will open a new tab in your browser for **Microsoft Defender**. 


Create a document fingerprint classifier:
1.	Sign in to the Microsoft 365 Compliance Center with your admin credentials.
2.	On the left navigation pane, click on "Data classification".
3.	On the data classification page, click on the "Trainable classifiers" tab.
4.	Click on the "+ Create classifier" button on the top right corner of the page.
5.	On the create classifier page, specify the name as "Health Record" and description as "Documents that contain health records".
6.	Choose the option "Use a document fingerprint" as the model type.
7.	Upload the template or the sample document that you want to use as the basis for the document fingerprint.


### Task 4 – Test the data classifiers

In this task, you will test the data classifiers by uploading sample documents to the SharePoint site. You will verify that the labels and the actions are applied correctly. You will then review the Content Explorer and Activity Explorer dashboards to see the overview and the details of the sensitive data and the activities in your organization.




