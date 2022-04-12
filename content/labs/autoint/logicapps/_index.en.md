+++
title = "Azure Logic Apps"
date = 2022-03-10T11:58:35-03:00
weight = 5
chapter = false
pre = "<b> </b>"
+++

### Azure Logic Apps 

Azure Logic Apps is a cloud-based platform for creating and running automated workflows that integrate your apps, data, services, and systems. With this platform, you can quickly develop highly scalable integration solutions for your enterprise and business-to-business (B2B) scenarios. As a member of Azure Integration Services, Azure Logic Apps simplifies the way that you connect legacy, modern, and cutting-edge systems across cloud, on premises, and hybrid environments.

The following list describes just a few example tasks, business processes, and workloads that you can automate using the Azure Logic Apps service:

- Schedule and send email notifications using Office 365 when a specific event happens, for example, an IDOC is received.

- Route and process customer orders across on-premises systems and cloud services.

- Move uploaded files from an SFTP or FTP server to Azure Storage and Datalakes.

All this can be accomplished with simple and Low Code-based flows that integrate Microsoft and non-Microsoft resources in a single, simple flow. 

![LAPS](/images/sap-logicapp01.png?height=300px)

To securely access and run operations on various data sources, you can use managed connectors in your workflows. Choose from many hundreds of connectors in an abundant and growing Azure ecosystem, for example:

- Azure services such as Blob Storage and Service Bus

- Office 365 services such as Outlook, Excel, and SharePoint

- Database servers such as SQL and Oracle

- Enterprise systems such as SAP and IBM MQ

- File shares such as FTP and SFTP

### What we will build

In this lab we will build an API and receives a JSON payload with the Sales Order to be queries on SAP and sends the required information via Outlook using native SAP and Office 365 integrations. 

Whenever this API is used, it triggers a Logic App (built with no code) that will analyze the payload, run a BAPI on SAP, process the response, build an HTML table and send it by email alongside with the BAPI JSON. 

You can see a sample of the lab below: 

{{< youtube wqMKEuQEmIA >}}

### Estimated Time for this Lab

This lab is estimated to take between 30 and 60 minutes. 

### Requirements

For this demo we will be using the following components from the Environment Setup: 

1. S/4HANA deployed from SAP CAL
2. On-premises data gateway installed and configured 
3. Azure subscription