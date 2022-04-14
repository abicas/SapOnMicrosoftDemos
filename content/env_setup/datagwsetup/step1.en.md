+++
title = "Remote Desktop Setup"
date = 2022-03-09T11:22:24-03:00
weight = 5
chapter = false
pre = "<b>1. </b>"
+++

In this section we will install the required components for Azure and Microsoft be able to connect to your SAP environment. 

This section is a summary of the guide [Install data gateway](https://docs.microsoft.com/en-us/azure/logic-apps/logic-apps-gateway-install) and [Connect to SAP systems](https://docs.microsoft.com/en-us/azure/logic-apps/logic-apps-using-sap-connector).

Connect to the Remote Desktop as on the previous step and using a browser on the Bastion Host, download 3 pieces of software (links might have changed, please check above guides for the most up-to-date links): 

- [.Net Framework latest version](https://dotnet.microsoft.com/en-us/download/dotnet-framework)
- [On-premises data gateway](https://aka.ms/on-premises-data-gateway-installer)
- [SAP Connector](https://docs.microsoft.com/en-us/azure/logic-apps/logic-apps-using-sap-connector#sap-client-library-prerequisites)

Install the **.Net Framework** following the standard process. Reboot the Bastion Host. 

Install the **On-premises Data Gateway** and configure it: 

1. Accept the default path and terms of use:
![DG01](/images/dg01.png?height=250px)
2. Once installation completes, we will register the gateway. Use the **same email address of the Azure subscription**. It will open a sign in window for you to complete authentication using your azure credentials.  
![DG02](/images/dg02.png?height=250px)
3. Select **Register a new gateway**:
![DG03](/images/dg03.png?height=250px)
4. Give it a name and define a recovery key:
![DG04](/images/dg04.png?height=350px)
5. Select the region. For this demos, **East US** is the prefered one: 
![DG05](/images/dg05.png?height=350px)
6. Installation on the Data gateway on the Bastion Host side is complete and you should see a screen similar to the one below, with both PowerBI and PowerApps showing up as Ready:
![DG06](/images/dg06.png?height=350px)

Install the **SAP .NET Connector** and make sure you select **Register WMI provider provider and install Assemblies  to GAC** 
![DG07](/images/dg_conn.png?height=350px)

Now, let's move to the Azure part, creating the Gateway on the cloud to interface with the on-premises data gateway.




