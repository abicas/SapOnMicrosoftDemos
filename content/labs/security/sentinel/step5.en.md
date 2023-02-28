+++
title = "Augmenting an Incident with GPT3"
date = 2022-03-14T14:22:13-03:00
weight = 11
chapter = false
pre = "<b>3. </b>"
+++

In the previous example we identified a security incident from SAP. 

In this demo we will build an automation to augment the incident with more information derived from GPT3.

**This demo depends on the steps we executed on the previous chapter. Don't skip it** 

#### Setting up permissions 

The SAPCAL resource group has a set of permissions that require some adjustments so we can create atuomations. 

In this step we will setup those permissions correctly so Sentinel can use its resources.

1. On the Azure portal, let's go to the Resource Groups resource page: 
![sso1](/images/sent-aut-1-1.png) 

2. On the Resource Groups resource page, click on the **<SAPCAL-xxxxxxxxxxxx>** resource group, select **Access Control (IAM)** and **Add role assingment**. 
![sso1](/images/sent-aut-1-2.png) 

3. We will do this **2X** for 2 sets of permissions: **Owner** and **Logic App Contributor**. 
    - Click on **Owner** Role and select the desired role. Click Next
    ![sso1](/images/sent-aut-1-3.png) 
    - Go to the **members** tab, and **Select Members**. Pick your user and click **Select**
    ![sso1](/images/sent-aut-1-4.png) 
    - Repeat it for the **Logic App Contributor** 
    ![sso1](/images/sent-aut-1-5.png) 
4. Let's make sure we have done it correcly: Click on the **Check Access** and confirm you have the 2 roles assigned. 
![sso1](/images/sent-aut-1-6.png) 

5. Then, go to Sentinel, click on **Settings**, then expand **Playbook Permissions**, click on **Configure permissions** and select the Resource Group **<SAPCAL-xxxxxxxxxxxx>**. Click Apply.
![sso1](/images/sent-aut-1-7.png) 


#### Creating our Automation

1. On the Sentinel page, under the Azure Portal, go to **Automations**, and **Create a Playbook with Incident Trigger** 
![sso1](/images/sent-aut-1-8.png) 

2. Pick the **<SAPCAL-xxxxxxxx>** resource group and name the Playbook **SAP_ADDGPTCOMMENTS**, also make sure to check to enable diagnostics so you can troubleshoot any issues. Click **Next: Connections** 
![sso1](/images/sent-aut-1-9.png?height=450px) 

3. Permissions for Sentinel should be setup. We will further add permissions to the Logic App. Click **Next: Review and Create**  
![sso1](/images/sent-aut-1-10.png?height=450px) 

4. Click **Create and continue to designer**  
![sso1](/images/sent-aut-1-11.png?height=450px) 

5. You will be brought to the Logic App Designer, where we will build the automation flow without creating a single line of code. It comes pre-populated with a Sentinel Incident as trigger. let's add the GPT3 action. Search for **GPT3**  and select **GPT3 completes your prompt** action: 
![sso1](/images/sent-aut-1-12.png) 

6. Then you will need to provide an API Key for OpenAI GPT3. Log in (or create an acount) in the [OpenAI page](https://openai.com/product), on the top right click on your user and **View API Keys** and then **Create a secret key**. Copy the value for the next step. 
![sso1](/images/sent-aut-1-40.png?height=350px) 
![sso1](/images/sent-aut-1-41.png?height=350px) 

7. Back to the Logic App, name the connection as **GPT3APIKEY** and add you key in the format **Bearer <YOURKEYHERE>** (example "Bearer djklcsjcsdkjcsdlkcsjdlcsd"). Click **Create**.
![sso1](/images/sent-aut-1-14.png) 

8. Let's add the prompt we need using the data from the Sentinel incident. 
- Prompt: "What should be the next investigation steps on security incident with description "<DESCRIPTION>" and title "<TITLE>" with involved entities "<ENTITIES>"
- Dynamic Content: **Incident Description**, **Incident Title**, **Entities**
- You can also expand max tokens from 100 to **250**
![sso1](/images/sent-aut-1-15.png) 

9. As a next step, we will tell to Logic Apps what to do with the GPT3 API response. Add an action **Add comment to incident v3** under Sentinel. 
![sso1](/images/sent-aut-1-16.png?height=400px) 

10. Use the Dynamic Content for **Incident ARM ID** and expand GPT3 dynamic content and select **Text**. 
![sso1](/images/sent-aut-1-17.png?height=450px) 


11. That is it, the Logic App is setup. It should be something like the picture below: 
![sso1](/images/sent-aut-1-20.png?height=500px) 

12. With our Logic App ready, we need to allow it to act on the Resource Groups resources. Still on the Logic App page, go to **Identity**,  enable **Status** and click on **Azure role assignments**. 
![sso1](/images/sent-aut-1-23.png) 

13. Click on the **Add role assignment** button and specify that you want to grant permissions based on **Resource Groups**, selecting **<SAPCAL-xxxxxxxx>** resource group and the Contributor role. Click Save and we are done in the Logic App page.  
![sso1](/images/sent-aut-1-24.png) 

12. Go back to Sentinel page, and let's set up a rule triggering the Logic App we just created. CLick on **Automation** and create an **Automation rule**. 
![sso1](/images/sent-aut-1-21.png?height=450px) 

13. Let's name the rule **Add_GPT3_Comment_rule**, select as Action **Run playbook**  and select the previously created **SAP_ADDGPTCOMMENTS** playbook. Click **Apply** 
![sso1](/images/sent-aut-1-22.png?height=450px) 

And that is it. We should have setup everything so that when an alert shows up and an incident is created, Sentinel will be able to append comments with additional incident information for first responder. Let's test it ! 

#### Generating an Incident

1. Log on to the Bastion Host and log on the SAP GUI (SAP Logon) with user **SAP*/Welcome1** (this will be a super restricted user log in incident)
![sso1](/images/sent-aut-1-26.png?height=450px) 

2. Go to TCODE **SU01** so we can create a new user
![sso1](/images/sent-aut-1-27.png?height=450px) 

3. Name the user **hacker01** and click on **User** 
![sso1](/images/sent-aut-1-28.png?height=450px) 

4. Give it a Last Name **hacker01** and move on to the Logon Data tab
![sso1](/images/sent-aut-1-29.png?height=450px) 

5. Set the password and confirm to **Welcome1**, c;lick **Save** and then log off be using the **Back button**
![sso1](/images/sent-aut-1-30.png?height=450px) 

6. Now, lets log in with the newly creater **hacker01/Welcome1** user, simulating another security incident
![sso1](/images/sent-aut-1-31.png?height=450px) 

7. It will ask for a new password. You can use **Microsoft1** and the new one here and proceed. Once logged in, you can log off, since the risk was already been recorded. 
![sso1](/images/sent-aut-1-32.png?height=450px) 

8. After a few minutes (5-10 minutes) the logs should have flown to Sentinel and an Incident should have been created. Go to Sentinel, on Overview (optionally you can disable the new interface), and select one recent incident. 
![sso1](/images/sent-aut-1-33.png?height=450px) 

9. On the incident details page, you can go to **Comments** tab
![sso1](/images/sent-aut-1-34.png?height=450px) 

10. If everything worked, you should see a comment added by the playbook with some augmentation regarding the security incident:
![sso1](/images/sent-aut-1-35.png?height=450px) 

Congratulations! In this example we were able to create a playbook, a rule and augment an incident with AI generated information upon a creation of an incident from SAP!
