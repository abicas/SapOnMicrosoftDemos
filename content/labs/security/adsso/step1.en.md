+++
title = "Setting up SAP"
date = 2022-03-14T14:22:13-03:00
weight = 5
chapter = false
pre = "<b>1. </b>"
+++

Before we start integrating SAP with Azure Active Directory for SSO, we need to setup SAP to allow this communication to happen. 

This section will show the steps required for this to be accomplished:

#### SAP Profile selection

1. Log on to the SAP BAstion host via Remote Desktop and look for open SAP GUI (SAP Logon) with user **BPINST/Welcome1**
2. Go to TCODE RZ10
![sso1](/images/sso-sapsetupA01.png?height=450px) 
3. We will change some parameters from the default SAP profile. Click on the **Profile** select **DEFAULT**, pick **Extended maintenance** and click on **CHANGE**
![sso1](/images/sso-sapsetupA02.png?height=450px) 
4. Click OK on the pop-up message
![sso1](/images/sso-sapsetupA03.png?height=150px) 

#### Setting up parameters 

We will change 3 parameters, following always the same procedure: 

5. Double-Click parameter **login/ticket_only_by_https** (default = 1)
![sso1](/images/sso-sapsetupA04.png?height=450px) 
6. Change its value to **0** and click on the **Back** button
![sso1](/images/sso-sapsetupA05.png?height=450px) 
7. Confirm the parameter change
![sso1](/images/sso-sapsetupA05b.png?height=150px) 

    Repeat the same procedure to 
    - Parameter: **icf/set_HTTPonly_flag_on_cookies** /  Value: **3**
    ![sso1](/images/sso-sapsetupA06.png?height=450px) 
    - Parameter: **icf/user_recheck** /  Value: **0**
    ![sso1](/images/sso-sapsetupA07.png?height=350px) 

8. Double check changes and click **Back Button**: 
-  **login/ticket_only_by_https** = **0**
-  **icf/set_HTTPonly_flag_on_cookies** = **3**
-  **icf/user_recheck** = **0**
![sso1](/images/sso-sapsetupA08.png?height=450px) 

9. Save the Profile Changes
![sso1](/images/sso-sapsetupA09.png?height=150px) 

10. Click on the **SAVE** button and select **No** for errors
![sso1](/images/sso-sapsetupA10.png?height=350px) 
11. Confirm new profile activation 
![sso1](/images/sso-sapsetupA11.png?height=150px) 
12. Click OK on the confirmation message
![sso1](/images/sso-sapsetupA12.png?height=150px) 

#### Reboot SAP 

In order for the changes become effective, we need to stop/start SAP. The simple way of doing this is going to the **Virtual Machines** under Azure Portal, selecting VMs SAP1 and SAP2 and clickgin **Restart**. It should take around 15 minutes for it to come back up, go grab a coffee. 
![sso1](/images/sso-sapsetupA13.png?height=250px) 

#### Confirming changes and activating parameters

**After the reboot**, we need a final step which is activating the parameters to the Client 100 into SAP:

1. Go to the SAP GUi on the Bastion Host and go to TCODE **SICF_SESSIONS** 
![sso1](/images/sso-sapsetup01.png?height=450px) 
2. Accept the message
![sso1](/images/sso-sapsetup02.png?height=450px) 
3. Check the parameters changed before the reboot, select **CLIENT 100** and click on **ACTIVATE BUTTON** 
![sso1](/images/sso-sapsetup03.png?height=450px) 

Alright ! This was the most complex part, changing SAP default profiel to accept SSO. 

On the next steps we will configure Azure AD and integrate with SAP. 




2. Create a new instance and provide the required information. Select the same region, vNet and subnet as SAP was deployed:
- Region: **East US** 
- vNET: **SAPCALDefault-eastus** 
- Subnet: **default** 
![monitoring1](/images/am02.png?height=450px) 
3. Do not worry about defining providers at this moment. Click on ****Review + Create** **
![monitoring1](/images/am03.png?height=450px)
4. Once the deployment is complete **Go to Resource** and let's start configuring the data Providers 
![monitoring1](/images/am05.png?height=450px)

Next steps will be divided by data provider. 
