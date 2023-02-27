+++
chapter = false
pre = "<b></b>"
title = "Microsoft Sentinel"
weight = 9
+++


### Microsoft Sentinel 
Microsoft Sentinel, also known as Azure Sentinel, is a cloud-native security information and event management (SIEM) service provided by Microsoft. It is designed to help organizations collect, analyze, and respond to security threats across their entire enterprise.

Microsoft Sentinel uses artificial intelligence and machine learning to identify potential security threats and offers a central location for monitoring security events and responding to incidents. It can collect data from a variety of sources, including Azure services, on-premises systems, third-party applications, and security devices.

The platform also provides security orchestration and automated response (SOAR) capabilities, which allow security teams to automate common response tasks and streamline incident response workflows. Additionally, Sentinel integrates with other Microsoft security services, such as Azure Active Directory and Microsoft Defender, to provide a comprehensive security solution.

With Microsoft Sentinel solution for SAP® applications you will be able to: 

- **Monitor all SAP system layers**: Gain visibility across business logic, application, database, and operating system layers with built-in investigation and threat detection tools.

- **Detect and automatically respond to threats**: Discover suspicious activity including privilege escalation, unauthorized changes, sensitive transactions, and suspicious data downloads with out-of-the-box detection capabilities.

- **Correlate SAP activity with other signals**: Accurately detect SAP threats with data correlation from all sources and SAP infrastructure.

- **Customize based on your needs**: Build your own threat detection solutions to monitor specific business risks to extend built-in security content.

![SSO](/images/sentinelsap01.jpg?height=450px)

For more details on the detected by Azure Sentinel for SAP, please check the updated [Product Documentation](https://learn.microsoft.com/en-us/azure/sentinel/sap/sap-solution-security-content).

The steps required to setup this lab are based on the [Deploy Microsoft Sentinel solution for SAP® applications](https://learn.microsoft.com/en-us/azure/sentinel/sap/deployment-overview) tutorial. 

### What we will build

In this lab we will integrate SAP S/4HANA with Microsoft Sentinel and demonstrate how we can identify secuerity incidents from within SAP. We will generate a couple of suspect activities on SAP and see it being reflected as security incidents that can be further automated. 

{{< youtube 8IyqdcN9d9Q >}}

### Estimated Time for this Lab

This lab is estimated to take between 180 minutes.

### Requirements

For this demo we will be using the following components from the Environment Setup: 

1. S/4HANA deployed from SAP CAL
2. Azure subscription
3. SAP S-User with download permissions for [SAP Netweaver SDK](https://aka.ms/sap-sdk-download)

{{% notice warning %}}
**SAP SOFTWARE DOWNLOAD**   
In order to be able to deploy the agent for Sentinel, we will need to download [SAP Netweaver SDK](https://aka.ms/sap-sdk-download) directly from SAP Downloads. Although it doesn't have a cost, it will require an SAP user with software download permissions.   
Please before continuing make sure you have an SAP user with proper permissions to download the required software or you won't be able to continue.
{{% /notice %}}