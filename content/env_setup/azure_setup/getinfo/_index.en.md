+++
title = "Get required information"
date = 2022-03-08T16:49:27-03:00
weight = 6
chapter = false
pre = "<b>3. </b>"
+++
In order to allow for SAP CAL to access your subscription, you will need some parameters. This section will explain where to find them. 

Copy those values to a temp text document so you can easily copy and paste later on. 

Go to your [Azure Portal](https://portal.azure.com) and follow the steps below: 

1. Go to **Subscriptions** and copy the **Subscription ID**
![Get Tenant ID](/images/getvalues0.png)
2. Select **Azure Active Directory**.
3. Select **Properties**.
4. Copy **Tenant ID**.
![Get Tenant ID](/images/getvalues1.png)
5. Still on Azure Active Directory, go to **App registrations** and select your application.
6. Copy **Application (client) ID**.
![Get Tenant ID](/images/getvalues2.png)
7. Select **Certificates & secrets**, then select **New client secret**.
![Get Tenant ID](/images/getvalues3.png)
8. Define a **name** for the secret and an expiration **3 Months**.
9. After adding the client secret, the value of the client secret is displayed. **Copy this value now because you aren't able to retrieve the client secret later.** You will provide the client secret value (as application password) with the application ID to sign in as the application. If you missed this step, delete the existing secret and create a new one. 

By that time you should have 4 pieces of info: 
- Azure Subscription ID
- Tenant ID
- Application  (client) ID
- Secret Value 

Now we will go to SAP CAL to setup the Azure access to deploy SAP S/4HANA in your subscription.
