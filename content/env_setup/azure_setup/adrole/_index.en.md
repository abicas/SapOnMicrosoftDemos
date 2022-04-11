+++
title = "Assign Role to Application"
date = 2022-03-08T16:49:27-03:00
weight = 6
chapter = false
pre = "<b>2. </b>"
+++

In this section we will add permissions and a role to the app registrations, allowing it to perform actions on your Azure subscription on your behalf: 

{{% notice warning %}}
In order to be able to deploy on your subscription, permissions used here will be quite broad. Make sure you go thru cleanup section to remove it after the labs, to avoid incidental usage of those credentials for non-authorized access to your subscription. In production environments, you should go thru the SAP and Microsoft best practices and setup access with the minimum required permissions and controls. 
{{% /notice %}}

1. Navigate to the level of scope you wish to assign the application to. For example, to assign a role at the subscription scope, select All services, General and **Subscriptions**.  
![Subscriptions](/images/subscriptions1.png)
2. Select the particular subscription to assign the application to.
3. Select **Access control (IAM)**
4. Select **Add role assignment**
![Add Role Assignment](/images/subscriptions2.png?height=350px)
5. Select the role you wish to assign to the application. To allow the application to execute actions like reboot, start and stop instances, select the **Contributor role**.
![Contributor](/images/subscriptions3.png)
6. On the Members tab, click on **Select members** and start typing the name of the App registration done on the previous step
7. Select **Review and Assign** to finish assigning the role. 

You will see your application in the list of users assigned to a role for that scope.

Your service principal is set up. You can start using it to run your scripts or apps. 
The next section shows how to get values that are needed when signing in programmatically.

