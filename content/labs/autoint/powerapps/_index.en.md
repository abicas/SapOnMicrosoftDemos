+++
title = "Power Apps"
date = 2022-03-10T11:58:35-03:00
weight = 7
chapter = false
pre = "<b> </b>"
+++

### Power Apps

Power Apps is a suite of apps, services, and connectors, as well as a data platform, that provides a rapid development environment to build custom apps for your business needs. Using Power Apps, you can quickly build custom business apps that connect to your data stored either in the underlying data platform (Microsoft Dataverse) or in various online and on-premises data sources (such as SAP, SharePoint, Microsoft 365, Dynamics 365, SQL Server, and so on).

Apps built using Power Apps provide rich business logic and workflow capabilities to transform your manual business operations into digital, automated processes. What's more, apps built using Power Apps have a responsive design and can run seamlessly in browser and on mobile devices (phone or tablet). Power Apps "democratizes" the business-app-building experience by enabling users to create feature-rich, custom business apps without writing code.

![PAPPS](/images/papps-sample.png?height=300px)

### What we will build

In this lab we will build an API and receives a JSON payload with the Sales Order to be queries on SAP and sends the required information via Outlook using native SAP and Office 365 integrations. 

Whenever this API is used, it triggers a Logic App (built with no code) that will analyze the payload, run a BAPI on SAP, process the response, build an HTML table and send it by email alongside with the BAPI JSON. 

You can see a sample of the lab below: 

{{< youtube YOIe_aw2VDw >}}

### Estimated Time for this Lab

This lab is estimated to take around 60 minutes. 

### Requirements

For this demo we will be using the following components from the Environment Setup: 

1. SAP Gateway Demo System
2. Azure subscription