+++
title = "Setting up Azure Monitor for SAP"
date = 2022-03-14T14:22:13-03:00
weight = 5
chapter = false
pre = "<b>1. </b>"
+++

In order to have SAP monitoring, we need to spin up an instance of Azure Monitoring. 

This section will show the steps required for that to be accomplished:

1. Log on to the [Azure Portal](https://portal.azure.com) and look for **Azure Monitor for SAP**
![monitoring1](/images/am01.png?height=450px) 
2. Create a new instance and provide the required information. Select the same region, vNet and subnet as SAP was deployed:
- Region: **East US** 
- vNET: **SAPCALDefault-eastus** 
- Subnet: **default** 
![monitoring1](/images/am02.png?height=450px) 
3. Do not worry about defining providers at this moment. Click on **+ Container**
![monitoring1](/images/am03.png?height=450px)
4. Once the deployment is complete **Go to Resource** and let's start configuring the data Providers 
![monitoring1](/images/am05.png?height=450px)

Next steps will be divided by data provider. 
