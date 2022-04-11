+++
title = "Azure Data Gateway Setup"
date = 2022-03-09T11:22:24-03:00
weight = 6
chapter = false
pre = "<b>2. </b>"
+++

In this section we will create the endpoint on Azure for the installed on-premises data gateway.

This section is a summary of the guide [Install data gateway](https://docs.microsoft.com/en-us/azure/logic-apps/logic-apps-gateway-install) and [Connect to SAP systems](https://docs.microsoft.com/en-us/azure/logic-apps/logic-apps-using-sap-connector).

Connect to the [Azure Portal](https://portal.azure.com) and follow the steps below:

1. Go to **On-premises Data Gateways**:
![DG01](/images/azdg01.png?height=250px)
2. Select **Add**
![DG02](/images/azdg02.png?height=150px)
3. Fill the required parameters. Make sure to **Select the same region as used on the installation (East US)** and **Select the name of the gateway** previously created that should be populated on the drop-down box. 
![DG03](/images/azdg03.png?height=450px)

Congratulations, you just setup communications between SAP and Azure in a secure and simple way. 

Now, let's head to the SAP Gateway Demo System setup. 



