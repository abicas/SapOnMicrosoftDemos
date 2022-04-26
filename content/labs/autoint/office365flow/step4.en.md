+++
title = "Testing the Automation"
weight = 10
pre = "<b>4. </b>"
chapter = false
+++

In this step we will test what we have built. 

The steps required are: 

1. After saving the flow (last step on section #3), click on **Test** on the top right corner
![auto0](/images/auto2-1.png?height=400)
2. Select **Manually** and click **Test**
![auto0](/images/auto2-2.png?height=400)
3. Click **Continue** 
![auto0](/images/auto2-3.png?height=400)
4. Finally click on **Run flow** 
![auto0](/images/auto2-4.png?height=400)
5. You will be redirected to the results page. Status should be **Your flow is running** (this test takes around 15s). 
![auto0](/images/auto2-5.png?height=400)
6. You can see the status on each step, and clicking them you can see the details of inputs and outputs of each step. 
![auto0](/images/auto2-19.png?height=400)
6. After 15s-20s your flow should have run successfully
![auto0](/images/auto2-6.png?height=400)
7. Let's check the inserted data ! Go to the [Fiori Launchpad](https://sapes5.sapdevcenter.com/sap/bc/ui5_ui5/ui2/ushell/shells/abap/FioriLaunchpad.html#Shell-home) and click on **Manage Products** 
![auto0](/images/auto2-7.png?height=300)
8. Filter by the 3 letter prefix you used on your Excel file (in this example PRD-) and click **Go**. You should see the inserted data. 
![auto0](/images/auto2-8.png?height=400)

Congratulations ! You just created an automation, with zero lines of code, to bulk create new products on SAP using existing ODATA interfaces by uploading a simple Excel file to OneDrive ! This lab can be customized to include different triggers, like a button on a Power App or an event, or an email with specific words on the subject... 