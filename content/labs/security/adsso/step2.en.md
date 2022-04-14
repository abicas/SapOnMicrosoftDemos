+++
title = "Setup Azure AD, Fiori & SSO"
date = 2022-03-14T14:22:13-03:00
weight = 6
chapter = false
pre = "<b>2. </b>"
+++

Now we will start to configure Azure Active Directory to be a provider for SAP. This will be a back and forth process where we configure AD, go to SAP to configure it, and return to finish AD configuration. 

1. Go to [Azure Portal](https://portal.azure.com) and select Azure Active Directory 
![sso1](/images/sso-nw00.png?height=150px) 

#### Setting Up Active Directory 

In case you don't have an AD configured already on your subscription, keep going. To use existing AD, jump to step #6. 

3. Let's create and Azure AD Tenant. Click on **Create** and select **Azure Active Directory**; click Next to **Configuration**  
![sso1](/images/sso-nw02.png?height=350px) 
4. On the configuration tab, give it an organization name (in the example **ADSAPDEMO**) and a UNIQUE Domain (in the example we used the same name). Make sure the Tenant is in the same region that your S/4HANA (In the example **United States**). Click **Review and Create**
![sso1](/images/sso-nw03.png?height=300px) 
5. Click **Create**
![sso1](/images/sso-nw04.png?height=300px) 

#### Creating our AD user

6. Go to **Users** on the AD Tenant left pane, and click on **ADD +**. 
![sso1](/images/sso-nw05.png?height=450px) 
7. Select **Create a User**, with parameters: 
    - Username: **bpinst** 
    - Name: **SAP Admin User** 
    - First Name: **BP**
    - Last Name: **INST**
    - Auto Generate Password 
    - Click show password and make note of the password. You will be prompted to change it on the first use. 
![sso1](/images/sso-nw06.png?height=550px) 

#### Configuring SAP Fiori SSO

Now we will go for the first part of the configuration, going to SAP and enabling SSO.

8. Go to the SAP Bastion Host, with Remote Desktop, and open SAP GUI. Go to TCODE **SAML2**. A Browser window will open. 
![sso1](/images/sso-nw13.png?height=450px) 
9. Logon user **BPINST/Welcome1** to the Netweaver WEB. Make sure client = 100. 
![sso1](/images/sso-nw14.png?height=450px) 
10. Click on **Create SAML2.0 Local Provider** 
![sso1](/images/sso-nw15.png?height=250px) 
11. Set Provider name to **http://S4H100** and lcick **Next**
![sso1](/images/sso-nw16.png?height=450px) 
12. Click Next again and Finish
![sso1](/images/sso-nw17.png?height=350px) 
13. Once creation is complete, it will show you the default parameters. Click on **Edit** and check **Include Certificate on Signature**. Click **Save**
![sso1](/images/sso-nw18.png?height=350px) 
14. Go to **METADATA** and select **Download Metadata** 
![sso1](/images/sso-nw19.png?height=350px) 
15. It will download a file called **metadata.xml** that will be used to configure Azure AD
![sso1](/images/sso-nw20.png?height=350px) 

#### Configuring Azure AD app for SAP Fiori SSO

16. On Azure portal, on the AD Tenant we created the user, click on **Enterprise applications** on the left panel and then **Add +** 
![sso1](/images/sso-nw07.png?height=450px) 
17. Use **SAP** as filter and select **SAP FIORI** App. Accept the default name and click **Create**
![sso1](/images/sso-nw08.png?height=350px) 
18. Click on **SAP Fiori** under All Applications
![sso1](/images/sso-nw09.png?height=300px) 
19. Inside SAP Fiori APP in Azure AD, select **Users and Groups** on the left panel, followed by **+ Add User/Group**
![sso1](/images/sso-nw10.png?height=450px) 
20. Let's select the AD user we created to this app. In Users, click **None Selected**,  pick **SAP Admin User**, click **Select** and **Assign**
![sso1](/images/sso-nw11.png) 
21. Now we will start to configure the connection to SAP. On the left panel, select **Single sign-on**  and click on **SAML**
![sso1](/images/sso-nw12.png) 
22. Instead of filling all the parameters, we will ise the **metadata.xml** file SAP generated to us. Click on **Upload metadata file** and select the **metadata.xml**. 
![sso1](/images/sso-nw21.png) 
23. On the right panel that will open, you just need to configure the **Sign on URL** to
**https://vhcals4hcs.dummy.nodomain** and click on **Save**. 
![sso1](/images/sso-nw22.png?height=450px) 
24. Next we will tell to Azure AD, how to handle the SAP username conversions (Azure AD bpinst@XXXXXX.onmicrosoft.com to SAP user BPINST). Click on **Edit** under Attributes and Claims
![sso1](/images/sso-nw23.png?height=350px) 
25. Click on the Unique User Identifier Claim to change its default configuration
![sso1](/images/sso-nw24.png?height=350px) 
26. Setup the following parameters: 
    - Source: **Transformation**
    - Transformation: **ExtractMailPrefix()**
    - Parameter 1: **user.userprincipalname**
    - Click **Add** and **Save**
![sso1](/images/sso-nw25.png)
27. Check for the change and download the **Base64 certificate** ("SAP Fiori.cer") and the **Federation Metadata XML** ("SAP Fiori.xml" file)
![sso1](/images/sso-nw26.png) 

##### Configuring SAP Fiori SSO with Azure AD on SAP 

Now that we did the Azure AD part, we need to finally go back to SAP to finish configuring the trust between the two authentication providers. 

28. Go back to the Bastion Host, under the SAML configuration webpage. Click on the **Trusted Providers** tab, and **Upload Metadata File** from Azure AD. 
![sso1](/images/sso-nw27.png?height=350px)
29. Select the **SAP Fiori.xml** file from Azure AD. Click **Next**.
![sso1](/images/sso-nw28.png?height=450px) 
30. Select the **SAP Fiori.cer** certificate file from Azure AD. Click **Next**.
![sso1](/images/sso-nw29.png?height=450px)
31. As an alias, use the name of the Azure AD tenant you used. Click **Next** 
![sso1](/images/sso-nw30.png?height=550px) 
32. Change **Digest Algorithm** to **SHA-256** and click **Next**
![sso1](/images/sso-nw31.png?height=550px) 
33. On Single Signon endpoints step, make HTTP POST is the default method. Click **Next**
![sso1](/images/sso-nw32.png?height=550px) 
34. Click **Next** until the last step (9) and click **Finish** 
![sso1](/images/sso-nw33.png?height=550px) 

35. It will now show Azure AD as a Trusted provider. Click on **Edit**, go to **Identity Federation**  and click **Add**. Select **Unspecified** and **OK**
![sso1](/images/sso-nw34.png?height=550px) 
36. Make sure parameters for **Unspecified** are as the picture below:
![sso1](/images/sso-nw35.png?height=550px) 
36. Again, click **Add**. Select **E-mail** and **OK**
![sso1](/images/sso-nw36.png?height=550px)
37. Make sure parameters for **E-mail** are as the picture below and click **Save**
![sso1](/images/sso-nw37.png?height=550px) 
38. Enable the SSO in SAP Fiori:
![sso1](/images/sso-nw38.png?height=550px) 

#### Linking Azure AD user and SAP user 

As the last step, we will need to tell SAP which SAP users corresponds to the Azure AD user. 

In this example we configured it so the Azure AD username (bpinst@XXXXX.onmicrosoft.com) must match SAP user's email. 

Let's go back to SAP GUI and configure it so we can test the SSO:

39. On SAP GUI, go to TCODE **SU01**
![sso1](/images/sso-nw39.png?height=550px) 
40. Select **BPINST** user and click the **Pencil** (change) icon
![sso1](/images/sso-nw40.png?height=350px) 
41. Scroll down the user properties under **Address** tab and include the Azure AD username (email) to the **E-mail Address** field. Click the **Save** icon (floppy disk)
![sso1](/images/sso-nw41.png?height=550px) 

PHEW ! That was a long one ! 

Now we have setup the trust between SAP Fiori and Azure AD, and taught SAP how to match Azure AD users for authentication. 

Let's go test it ! 