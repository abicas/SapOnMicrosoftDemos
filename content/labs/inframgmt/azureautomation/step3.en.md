+++
title = "Starting SAP"
date = 2022-03-15T15:55:06-03:00
weight = 8
chapter = false
pre = "<b>3. </b>"
+++

{{% notice warning %}}
This assumes that your SAP envinronment is deployed but suspended, with VMs in **Stopped** state. 

In case your SAP is running, go to SAP CAL and suspend the environment so we can start it with the runbook. 
{{% /notice %}}

With Azure Automation configured and the VMs tagged, we can execute the main runbook to start SAP 

This section will show the steps required for that to be accomplished:

#### Executing the Start-SAPSystem Runbook 

1. Go to the Azure Automation Account **SAPAutomationAcc** and select **Runbooks** on the left panel. Click on **Start-SAPSystem**. 
![ss1](/images/startstop-28.png)

1. On the Runbook page, go to **Overview** and click **Start**. You will need to provide the following parameters: 
- SAPSID = **S4H**
- WAITFORSTARTTIMEOUTINSECONDS: **leave blank**
- CONVERTDISKSTOPREMIUM: **False** 
- PRINTEXECUTIONCOMMAND: **True** 
- Click **OK** 
![ss1](/images/startstop-29.png)

#### Monitoring Execution

3. You will be taken to the Job Status page. Click on the **All Logs** view and select **Refresh**. This process takes around 20 minutes, so you can check back periodically until status changes from running to Completed
![ss1](/images/startstop-30.png)
4. During the Runbook execution, you will be able to see the commands it is issuing on the servers to start/stop SAP, App Server and HANA Database and check its status. 
![ss1](/images/startstop-33.png)
5. You can also check the **Outputs** view, with the script output displayed.
![ss1](/images/startstop-35.png)
![ss1](/images/startstop-36.png)

Congratulations, you have started your SAP landscape automatically ! Later on you will learn how to schedule this so you can start SAP in the morning and stop it during off-work hours. 