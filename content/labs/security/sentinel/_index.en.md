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

![SSO](/images/sso-sample.png?height=300px)

The general SSO flow can be seen below: 

![SSO](/images/sso-flow.png?height=300px)
1. User access URL protected by SSO. In the example we will use SAP Fiori
2. SAP Fiori, redirects to the SSO provider (Azure) login screen
3. User provides authentication details (username/password) from AD
4. Credentials are generated and exchanged 
5. Authenticated users have credentials generated and sent to SAP Fiori 
6. SAP Fiori checks the credentials and allows access to itself 


This lab is based on the [Deploy Microsoft Sentinel solution for SAP® applications](https://learn.microsoft.com/en-us/azure/sentinel/sap/deployment-overview) tutorial. 

### What we will build

In this lab we will integrate SAP S/4HANA with Microsoft Sentinel and demonstrate how we can identify secuerity incidents from within SAP. 

{{< youtube 8IyqdcN9d9Q >}}

### Estimated Time for this Lab

This lab is estimated to take between 120 minutes.

### Requirements

For this demo we will be using the following components from the Environment Setup: 

1. S/4HANA deployed from SAP CAL
2. Azure subscription