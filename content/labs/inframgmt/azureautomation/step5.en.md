+++
title = "Schedule Automation"
date = 2022-03-15T15:55:06-03:00
weight = 10
chapter = false
pre = "<b>5. </b>"
+++

With Azure Automation configured, the VMs tagged, and the Runbooks tested, we can schedule their execution for scheduled automation. 

This section will show the steps required for that to be accomplished:

{{% notice info %}}
In this example we will show you how to schedule the Stop-SAPSystem runbook. You can follow the same steps for other runbooks and SIDs. 
{{% /notice %}}


1. Go to the Azure Automation Account **SAPAutomationAcc** and select **Schedules** on the left panel. Click on **Add a schedule**. Provide the following parameters: 
- Name: **Shutdown SAPDEV** 
- Description: **Shutdown SAPDEV** 
- Starts: **Tomorrow @ 6:00PM** 
- Timezone: **Your timezone** 
- Recurrence: **Recurring** 
- Recur Every: **1 Day**
- CLick **Create** 
![ss1](/images/startstop-40.png)

2. Ok, so far we created the schedule but we haven't specified the runbook to be executed. Once the Schedule is created, click on **Runbooks** on the left panel. 
![ss1](/images/startstop-41.png)

3. Pick the **Stop-SAPSystem** Runbook.
![ss1](/images/startstop-42.png)

4. On **Overview** click on **Link to schedule**. 
![ss1](/images/startstop-43.png)

6. Click on **Link a schedule to your Runbook** 
![ss1](/images/startstop-44.png)

6. Pick the **Shutdown SAPDEV** schedule we just created. 
![ss1](/images/startstop-45.png)

7. Click on **configure parameters and run settings** 
![ss1](/images/startstop-46.png)

8. Set the following parameters, just we did on the manual execution: 
- SAPSID: **S4H** 
- SOFTSHUTDOWNTIMEINSECONDS: **150** 
- CONVERTDISKTOSTANDARD: **False** 
- PRINTEXECUTIONCOMMAND: **True** 
- Click **OK** 
![ss1](/images/startstop-47.png)

All set ! At 6PM tomorrow (and every day after that) Azure Automation will run the runbook with the provided parameters. 

You can check the Job executions by clicking on the Automation Account **SAPAutomationAcc** and selecting **Jobs** on the left panel.  
![ss1](/images/startstop-49.png)

Once you pick the desired execution, you can see the details just like we did on the manual execution. 
![ss1](/images/startstop-48.png)

Congratulations, you have scheduled your SAP to be stopped automatically using a Runbook! 