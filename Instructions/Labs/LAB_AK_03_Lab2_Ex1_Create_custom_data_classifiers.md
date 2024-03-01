In this lab exercise, you will create a custom data classifier, a custom trainable classifier, and a document fingerprint classifier, and use them to apply labels and actions to data in your organization.
Here are the steps to complete the lab exercise:
1.	Create a custom data classifier that applies the label "Sensitive" to data that contains the word "secret". Configure the data classifier to encrypt the data and add a watermark that says "Sensitive".
2.	Create a custom trainable classifier that identifies documents that contain resume information. Use the seed data that you have prepared to train the model. Configure the trainable classifier to apply the label "Resume" to the documents and delete them after 30 days.
3.	Create a document fingerprint classifier that detects documents that contain health records based on the template or the sample document that you have. Configure the document fingerprint classifier to apply the label "Health Record" to the documents and notify the admin.
4.	Test the data classifiers and the trainable classifiers by uploading some sample documents to the SharePoint site. Verify that the labels and the actions are applied correctly.
5.	Review the Content Explorer and Activity Explorer dashboards to see the overview and the details of the sensitive data and the activities in your organization.

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
Create a document fingerprint classifier:
1.	Sign in to the Microsoft 365 Compliance Center with your admin credentials.
2.	On the left navigation pane, click on "Data classification".
3.	On the data classification page, click on the "Trainable classifiers" tab.
4.	Click on the "+ Create classifier" button on the top right corner of the page.
5.	On the create classifier page, specify the name as "Health Record" and description as "Documents that contain health records".
6.	Choose the option "Use a document fingerprint" as the model type.
7.	Upload the template or the sample document that you want to use as the basis for the document fingerprint.
