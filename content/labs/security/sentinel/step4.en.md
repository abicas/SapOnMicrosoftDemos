+++
title = "Detecting 1st vulnerability"
date = 2022-03-14T14:22:13-03:00
weight = 10
chapter = false
pre = "<b>3. </b>"
+++

We have the logs being pushed to Sentinel. Let's configure the data connectors to handle SAP logs on Azure Sentinel.

In this first example we will monitor for a security vulnerability regarding user creation, where an users create a new user using SAP transaction SU01 and then log in using the newly created user from the same IP. This might be a Discovery technique used by attackers. 

#### Creating our rule

During the first part of this tutorial, we created a Log Analytics, connected it with Sentinel and installed the connector for SAP logs. 

Now we will create our first rules so we can identify security incidents from the logs. 

1. If not already on the connector page, go to Sentinel, select the Log Analytics we created, click on Data Connectors and hit refresh while filtering for SAP. Head over to the connector page to see more details
![sso1](/images/sent5-5.png) 

2. On the connector page, click on the **Next steps** tab on the right, by the bottom of the page you will be able to see Analytics templates. Click on the **go to analytics tempaltes** 
![sso1](/images/sent6-1.png) 

3. Under **Rule templates**, look for **SAP - User Creates and uses a new user** template. Once you click it it will bring more details and a button to create a rule to monitor for this threat. click on **Create Rule** button
![sso1](/images/sent6-2.png) 

4. On the **General tab** you can see more details about the rule we will be creating and adjust its parameters in case you need. Change the Status to **Enabled** and click on **Next: Set rule logic**. 
![sso1](/images/sent6-3.png?height=450px) 

5. On the **Set rule logic** you can see more details about the rule we will be creating, like the KQL used to query the logs and identify the issue. Scrool down on the page and change the query to **Run every 5 minutes** so we don't have to wait for 1 hour which is the default time it takes to scan the logs again. Click on **Next: Incident Settings**.
![sso1](/images/sent6-4A.png?height=450px) 
![sso1](/images/sent6-4B.png?height=450px) 

6. Here you can group alerts into a single incident. Nothing to be changed, click on **Next: Automated response**. 
![sso1](/images/sent6-5.png?height=450px) 

7. Here we can link automation rules to react automatically upon and alert or incident. In this demo we won't be automating anything, so we can move on and click on **Next: Review**
![sso1](/images/sent6-6.png?height=450px) 

8. Review and Click **Create**  
![sso1](/images/sent6-7.png?height=450px) 

#### Generating an incident 

Now that we have a rule created to watch for a user creating and using a new user from the same IP, let's test it on SAP. 

1. Log on to the Bastion Host and log on the SAP GUI (SAP Logon) with user **BPINST/Welcome1**
![sso1](/images/sent3-2.png?height=450px) 

2. Go to TCODE **SU01** for user maintenance
![sso1](/images/sent6-9.png?height=350px) 

3. Let's create a user named **demohack1** and click on **User** button. 
![sso1](/images/sent6-10.png?height=350px) 

4. Under Address tab, fill Last name with **demohacker1** and go to **Logon Data** tab.  
![sso1](/images/sent6-11.png?height=350px) 

5. FIll the password as **Microsoft1** and repeat it. Click **Save** Button
![sso1](/images/sent6-12.png?height=350px) 

6. Log off from SAP GUI by using the **Back** button, multiple times. 
![sso1](/images/sent6-13.png?height=150px) 

7. Log in with the newly created user **demohack1** and password **Microsoft1** 
![sso1](/images/sent6-14.png?height=350px) 

8. That is it! We should have generated an action that trigger an alert. You can log off using the back button. 
![sso1](/images/sent6-15.png?height=350px) 

9. Back on Sentinel, go to **Overview** and after a couple of minutes you should see the alert and incident show up. You can use the refresh button in case you need it. Once it shows up, click on it, under Recent Incidents.
![sso1](/images/sent6-16.png?height=450px) 

10. Here you can see the newly created incident details, like the Status and Owner. You can also see some insights like the Entities related (user BPinst that created demohack1, S4H SAP instance, and similar incidents). From here you could reassign the incident to a specialist, change the severity, include more details upon investigation... Click on **Investigate** button on the bottom left. 
![sso1](/images/sent6-18.png?height=450px) 

11. Here you can see a relationship graph of the involved entities. For more complex incidents you will be able to see more elaborate graphs. In this snapshot, we have already tested with a DEMO02 user so the same incident is related to more than one new user. 
![sso1](/images/sent6-19.png?height=450px) 


Allright! In this simple example we were able to create a rule and trigger a simple incident from SAP all the way to Sentinel ! Congrats ! 

On the next example we will go for more elaborate Rules. 
