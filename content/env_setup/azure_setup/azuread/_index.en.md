+++
title = "Create and Azure Active Directory application"
date = 2022-03-08T16:34:27-03:00
weight = 5
chapter = false
pre = "<b>1. </b>"
+++

First of all, we will need to create an Active Directory app registration that will be used by SAP CAL: 

1. Sign in to your Azure Account through the [Azure Portal](https://portal.azure.com)
2. Select **Azure Active Directory**
3. Select **App Registrations**
![App Registrations](/images/app-reg1.png)
4. Select **New Registration**
![New Registration](/images/app-reg2.png?height=100px)
5. Provide a name, accept defaults and select **Register**
![Register](/images/app-reg3.png?height=450px)

So far this app registration can't do much. Now let's add a role to this application.

