+++
title = "Create Sentinel"
date = 2022-03-14T14:22:13-03:00
weight = 5
chapter = false
pre = "<b>1. </b>"
+++

Before we start integrating SAP with Microsoft Sentinel, we need to setup components to allow this communication to happen. 

This section will show the steps required for this to be accomplished:

#### Setting up Log Analytics

1. Go to [Azure Portal](https://portal.azure.com), click on **Create Resource** and look for  **Log Analytics Workspaces**
![sent1](/images/sent1-1.png?height=250px) 
2. Click **Create**
![sent2](/images/sent1-2.png?height=150px) 
3. Fill in the required informations: 
    - Subscription: **SELECT YOUR SUBSCRIPTION** 
    - Resource Group: **SAP CAL Resource Group** 
    - Name: **SAPLogAnalyticsWorkspace**
    - Region: **East US**
    - Click on **Review + create** and then **Create**
![sent3](/images/sent1-3.png) 

#### Creating a Microsoft Sentinel workspace

1. Go to [Azure Portal](https://portal.azure.com), click on **Create Resource** and look for  **Microsoft Sentinel**
![sent4](/images/sent2-1.png?height=200px) 
2. Click **Create**
![sent2](/images/sent2-2.png?height=150px) 
3. Select the previously created **SAPLogAnalyticsWorkspace** and click **Add** 
![sent2](/images/sent2-3.png?height=450px) 
4. If this is your first Microsoft Sentinel, accept the Trial 
![sent2](/images/sent2-4.png?height=150px) 
5. On the **Get Started** click on **go to Content Hub** so we can add SAP log model to Sentinel
![sent2](/images/sent2-5.png?height=350px) 
6. Look for **SAP**, select the Solution and click **Install**
![sent2](/images/sent2-6.png?height=350px) 
7. On the next screen, click **Create**
![sent2](/images/sent2-7.png?height=350px) 
8. Fill in the required informations: 
    - Subscription: **SELECT YOUR SUBSCRIPTION** 
    - Resource Group: **SAP CAL Resource Group** 
    - Deployment Target Workspace: **SAPLogAnalyticsWorkspace**
    - Click on **Review + create** and then **Create**
![sent3](/images/sent2-8.png?height=450px) 


Alright! With that we set up a place to receive the logs sent by SAP and prepared Sentinel to understand these logs. 

On the next steps we will configure SAP to send those logs. 

