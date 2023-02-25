+++
title = "Testing SSO"
date = 2022-03-14T14:22:13-03:00
weight = 9
chapter = false
pre = "<b>3. </b>"
+++

Now that the configuration steps are done, we are ready to test the SSO in action. 

All the operations will be done on the Bastion Host once, even with internet access, name resolution and security certificates are generated using the internal network names by SAP CAL.

1. From the Bastion Host, open an internet browser window and navigate to [https://vhcals4hcs.dummy.nodomain:44301/sap/bc/ui2/flp](https://vhcals4hcs.dummy.nodomain:44301/sap/bc/ui2/flp). Confirm that it no longer asks for User and password, instead offering a choice of identity provider, in this case **ADSAPDEMO** as we specified on Azure AD. Click **Continue**. 
![sso1](/images/sso-nw44.png?height=550px) 
2. You should be redirected to the Microsoft AD portal. Provide the Azure AD email address as created on the previous steps. 
![sso1](/images/sso-nw45.png?height=550px) 
3. Use the initial password provided by Azure AD (and copied to a scratch area in the previous steps) if this is your first logon
![sso1](/images/sso-nw46.png?height=550px) 
4. If this is your first logon with this user, Azure AD will ask you to change your password. 
![sso1](/images/sso-nw47.png?height=550px) 
5. Once logon is sucessfull, you will be redirected by Azure AD to the SAP Fiori page. In the background, Azure AD exchanged security keys and certificates with SAP Fiori that now recognizes this access as a valid SAP user. 
![sso1](/images/sso-nw48.png?height=150px) 
6. Once SAP Fiori has launched, click on the top right icon, and make sure it is logged on using the right SAP user **BPINST**
![sso1](/images/sso-nw49.png?height=150px) 

Congratulations ! You have enabled SSO between SAP Fiori and Microsoft Azure AD and now users can log in to SAP using their corporate credentials, MFA, and any other security rules defined by your organization. 