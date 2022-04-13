+++
title = "Single Sign On"
date = 2022-03-14T14:13:05-03:00
weight = 5
chapter = false
pre = "<b></b>"
+++

### Azure Active Directory Single Sign On (SSO)
Single sign-on is an authentication method that allows users to sign in using one set of credentials to multiple independent software systems. Using SSO means a user doesn't have to sign in to every application they use. With SSO, users can access all needed applications without being required to authenticate using different credentials.

Azure AD can be used to provide SSO capabilities to SAP, either on the cloud (BTP, SCP, Sucess Factors, among many other solutions) or on your on-premises environment, all while using the same corporate standards for security, like password complexity, Multi-Factor Authentication, Conditional Login, ... 

![SSO](/images/sso-sample.png?height=300px)

The general SSO flow can be seen below: 

![SSO](/images/sso-flow.png?height=300px)
1. User access URL protected by SSO. In the example we will use SAP Fiori
2. SAP Fiori, redirects to the SSO provider (Azure) login screen
3. User provides authentication details (username/password) from AD
4. Credentials are generated and exchanged 
5. Authenticated users have credentials generated and sent to SAP Fiori 
6. SAP Fiori checks the credentials and allows access to itself 


This lab is based on the [Azure Active Directory single sign-on (SSO) integration with SAP Fiori](https://docs.microsoft.com/en-us/azure/active-directory/saas-apps/sap-netweaver-tutorial#configure-sap-netweaver-using-saml) tutorial. 

### What we will build

{{< youtube 8IyqdcN9d9Q >}}

### Estimated Time for this Lab

This lab is estimated to take between 60 minutes.

### Requirements

For this demo we will be using the following components from the Environment Setup: 

1. S/4HANA deployed from SAP CAL
2. Azure subscription