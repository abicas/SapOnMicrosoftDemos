+++
title = "Setup VM Tags"
date = 2022-03-15T15:55:06-03:00
weight = 7
chapter = false
pre = "<b>2. </b>"
+++

In order for Azure Automation to be able to identify the correct VMs that need to be started or stopped, we need to add a few Tags to them. This example is aimed at a simple scenario like the one deployed by SAP CAL or a DEV environment. Please see [the complete documentation](https://github.com/Azure/SAP-on-Azure-Scripts-and-Utilities/tree/main/Start-Stop-Automation/Automation-Backend) for more information.

This section will show the steps required for that to be accomplished:

#### Adding Tags 

1. Log on to the [Azure Portal](https://portal.azure.com), go to **Virtual Machines** and select the HANA VM (**XXXX-SAP1**) 
![SS1](/images/startstop-18.png?height=250px) 
2. Click on **Tags** on the left pane and add the following: 
- SAPApplicationInstanceNumber: 1
- SAPApplicationInstanceType: SAP_ASCS
- SAPDBMSType: HANA
- SAPHANAInstanceNumber: 02 
- SAPHANASID: HDB
- SAPSystemSID: S4H
- Click **Apply** 
![SS1](/images/startstop-19.png?height=400px) 
3. Go back to the **Virtual Machines** page and select the App server VM (**XXX-SAP2**)
![SS1](/images/startstop-19b.png?height=250px) 
4. Click on **Tags** on the left pane and add the following: 
- SAPApplicationInstanceNumber: 1
- SAPApplicationInstanceType: SAP_J
- SAPSystemSID: S4H
- Click **Apply** 
![SS1](/images/startstop-19c.png?height=400px) 


Congratulations, you have finished configuring the VMs with tags so that Azure Automation can correctly coordinate the operations to start/stop SAP. On the next sectiopn we will start the SAP deployed from SAP CAL. 
