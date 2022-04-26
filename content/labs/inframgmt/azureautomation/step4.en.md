+++
title = "Stopping SAP"
date = 2022-03-15T15:55:06-03:00
weight = 9
chapter = false
pre = "<b>4. </b>"
+++

{{% notice warning %}}
This assumes that your SAP envinronment is deployed and running, with VMs in **Running** state. 

In case your SAP is stopped check the previous step (#3) on this section  so you can start it or start it using SAP CAL. 
{{% /notice %}}

With Azure Automation configured and the VMs tagged, we can execute the main runbook to stop SAP 

This section will show the steps required for that to be accomplished:

#### Executing the Stop-SAPSystem Runbook 

1. Go to the Azure Automation Account **SAPAutomationAcc** and select **Runbooks** on the left panel. Click on **Stop-SAPSystem**. 
![ss1](/images/startstop-38a.png)

2. On the Runbook page, go to **Overview** and click **Start**. You will need to provide the following parameters: 
- SAPSID = **S4H**
- SOFTSHUTDOWNTIMEOUTINSECONDS: **leave blank**
- CONVERTDISKSTOSTANDARD: **False** 
- PRINTEXECUTIONCOMMAND: **True** 
- Click **OK** 
![ss1](/images/startstop-38b.png)

3. During the SAP shutdown phase, a warning message will be displayed to the users on SAP GUI
![ss1](/images/startstop-37.png)

4. Monitor the status just like we did on the Start runbook and wait for it to change status to **Completed**. This ordered shutdown can take up to 30 minutes. 
![ss1](/images/startstop-38c.png)

Congratulations, you have stopped your SAP landscape automatically using a Runbook! On the next section you will learn how to schedule this so you can start SAP in the morning and stop it during off-work hours. 