+++
title = "Microsoft On-premises Data Gateway Installation"
date = 2022-03-09T11:21:23-03:00
weight = 7
chapter = false
pre = "<b></b>"
+++

Once SAP is installed and access is working, we need to install the required components to allow for Microsoft services to interact with SAP S/4HANA environments.

The on-premises data gateway acts as a bridge to provide quick and secure data transfer between on-premises data (data that isn't in the cloud) and several Microsoft cloud services. These cloud services include Power BI, PowerApps, Power Automate, Azure Analysis Services, and Azure Logic Apps. By using a gateway, organizations can keep databases and other data sources on their on-premises networks, yet securely use that on-premises data in cloud services.

![DATAGW](/images/on-prem-data-gateway-diagram.png?height=300px)

This section will go thru the steps required to get this software installed and accessing Azure resources.

### What you will need

1. Sucessfull deployment of S/4HANA and access validated in the previous step

### Expected duration

This section is estimated to last no longer than 30 minutes

### Additional Links and Infos

For future reference, part of this content was developed by taking information from: 

[What is an On-premises Data Gateway](https://docs.microsoft.com/en-us/data-integration/gateway/service-gateway-onprem)

[Install the On-premises Data Gateway](https://docs.microsoft.com/en-us/data-integration/gateway/service-gateway-install)

[Use the On-premises Data Gateway](https://docs.microsoft.com/en-us/data-integration/gateway/service-gateway-app)

[On-premises Data Gateway setup guide](https://docs.microsoft.com/en-us/azure/logic-apps/logic-apps-using-sap-connector)

[SAP ERP Connectors](https://docs.microsoft.com/en-us/connectors/saperp/)

