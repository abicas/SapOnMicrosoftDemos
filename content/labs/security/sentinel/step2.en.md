+++
title = "Setup SAP"
date = 2022-03-14T14:22:13-03:00
weight = 6
chapter = false
pre = "<b>2. </b>"
+++

Now we will prepare and configure SAP to send the logs to Sentinel Agent, which will be deployed later on. 

#### Downloading  SAP Change Requests

1. Log on to the SAP S/4HANA host via SSH (or Putty)
```sh
ssh -i SAPCALKey.pem root@S4HANAIP
```
2. On the host console, create a directory and download the Change Requests:
```sh
cd
mkdir CRs
cd CRs
wget -q https://raw.githubusercontent.com/Azure/Azure-Sentinel/master/Solutions/SAP/CR/K900271.NPL
wget -q https://raw.githubusercontent.com/Azure/Azure-Sentinel/master/Solutions/SAP/CR/R900271.NPL
wget -q https://raw.githubusercontent.com/Azure/Azure-Sentinel/master/Solutions/SAP/CR/K900202.NPL
wget -q https://raw.githubusercontent.com/Azure/Azure-Sentinel/master/Solutions/SAP/CR/R900202.NPL
wget -q https://raw.githubusercontent.com/Azure/Azure-Sentinel/master/Solutions/SAP/CR/K900201.NPL
wget -q https://raw.githubusercontent.com/Azure/Azure-Sentinel/master/Solutions/SAP/CR/R900201.NPL
```
3. Let's set permissions so SAP can read the files and move then to the sap/trans folder:
```sh
chown s4hadm:sapsys *.NPL
cp -p K*.NPL /usr/sap/trans/cofiles/
cp -p R*.NPL /usr/sap/trans/data/
``` 

Here is an example of what you should see: 
![sso1](/images/sent3-1.png?height=350px) 

#### Setting up SAP Change Requests

1. Log on to the Bastion Host and log on the SAP GUI (SAP Logon) with user **BPINST/Welcome1**
![sso1](/images/sent3-2.png?height=450px) 
2. Go to TCODE **STMS_IMPORT**
![sso1](/images/sent3-3.png?height=450px) 
3. The next steps will be repeated for all 3 CRs we downloaded: NPLK900201, NPLK900202 and NPLK900271
4. Click on **Extras** on the menu bar, then **Other Requests** and then **Add** 
![sso1](/images/sent3-4.png?height=350px) 
5. Click on the button beside **Request** 
![sso1](/images/sent3-5.png?height=350px) 
6. Select the first Request and click on the green checkmark
![sso1](/images/sent3-6.png?height=500px) 
7. Click on the green checkmark and confirm 
![sso1](/images/sent3-7.png?height=250px) 
![sso1](/images/sent3-8.png?height=150px) 
8. **REPEAT THE PROCESS 4-7 FOR THE OTHER 2 REQUESTS**

9. Now let's **Import all Requests**, by clicking on the icon
![sso1](/images/sent3-9.png?height=350px) 
10. Setup the Import process: 
- Target Client: **100** 
- Click on **Options** and check **Igonre invalid component version** 
- Click on the Green checkmark and confirm on the pop up
![sso1](/images/sent3-10.png?height=450px) 
![sso1](/images/sent3-11.png?height=250px) 

11. To make sure the requests installed correctly, go to the **Goto** and then **Import History** 
![sso1](/images/sent3-12.png?height=350px) 
12. You should see a screen similar to this, with a green status for Sample Role and a warning for the other 2. Return to the main screen using the **Back** button
![sso1](/images/sent3-13.png?height=350px) 

Now, with the Change Requests implemented, we can create the ROLE and then the USER for Senntinel to read the logs from SAP. 

#### Setting up the Role for Sentinel 

With CR NPLK900271, a role called /MSFTSEN/SENTINEL_CONNECTOR was created for Sentinel. Let's adjust it.

1. Go to TCODE **PFCG**
![sso1](/images/sent4-1.png?height=450px) 
2. Fill in the Role parameter with **/MSFTSEN/SENTINEL_CONNECTOR** and click on the **Change** button (Pencil icon)
![sso1](/images/sent4-2.png?height=450px) 
3. Click on the **Authorizations** tab and then on the **Change Authorization Data** button
![sso1](/images/sent4-3.png?height=450px) 
4. Note that the status is **Unchanged**. Click on the **Generate** button and the status should change. CLick on the **Back** button
![sso1](/images/sent4-4.png?height=350px) 
5. Authorizations Tab should be green and Last Changed date should have been updated. Click on **Save**
![sso1](/images/sent4-5.png?height=350px) 

#### Setting up the User for Sentinel

Now we can create the user for Sentinel on SAP with the proper permissions.

1. Go to TCODE **SU01** on the main screen of SAP GUI.
![sso1](/images/sent4-6.png?height=450px) 
2. On the Logon Data tab, fill in the User parameter with **SENTINELUSR** and click on the **Technical User** button
![sso1](/images/sent4-7.png?height=450px) 
3. Change the User Type to **System** and on Password use **Microsoft01** twice.
![sso1](/images/sent4-8.png?height=450px) 
4. Click on the **Roles** tab and it should be empty. On the first Line fo the Roles, click on the search button and search for the Role that we created **/MSFTSEN/SENTINEL_CONNECTOR** and click on the green checkmark. 
![sso1](/images/sent4-9.png?height=350px) 
5. Mark the Role with a check and click on the green checkmark
![sso1](/images/sent4-10.png?height=350px) 
6. Status should be green. Click **Save**
![sso1](/images/sent4-11.png?height=350px) 

Now we have setup the permissions for Sentinel to get the logs from SAP. 

As a final step, we need to enable Audit Logs on SAP, since this is not the default on the SAP CAL deployment. 

#### Setting up Audit Logs on SAP

1. Go to TCODE **RSAU_CONFIG** on the main screen of SAP GUI.
![sso1](/images/sent4-12.png?height=450px) 
2. Click on **Parameter**, then on the **Edit** button (Glasses and pencil icon), enable **Statitc security audit active** and hit **Save**
![sso1](/images/sent4-13.png?height=450px) 
3. Right-click on the **Static Configuration** menu item and then select **Create Profile**
![sso1](/images/sent4-14.png?height=450px) 
4. Name the profile **Default** and as Description put **Default with Audit**. Click **Save** button
![sso1](/images/sent4-15.png?height=350px) 
5. The new profile will show up under Static Configuration. Right click it and select **Create Filter**
![sso1](/images/sent4-16.png?height=350px) 
6. Make the following changes: 
- Enable **Filter for recording active** 
- Client = *
- User = * 
- Select **Classic event selection**
- Mark **All Audit Classes**
- Click **Save**
![sso1](/images/sent4-17.png?height=650px) 
7. Right click the Default profile again and select **Activate**. Confirm the change.
![sso1](/images/sent4-18.png?height=450px) 
![sso1](/images/sent4-19.png?height=150px) 
8. Filter under Default should show up with a green icon.
![sso1](/images/sent4-20.png?height=350px) 
8. Finally, we need to reboot SAP for changes to be in effect. On the **SAP CAL** dashboard on your web browser, clieck on **Appliance**, select your deployment, and on the right side, click on the **...** and select **Reboot** so changes can be in effect. 
![sso1](/images/sent4-21.png) 


That was a long one. It needs to be done just once. 

Go grab a coffee and a snack and give it 10 minutes for SAP to reboot and come back online with the changes and logs activated. 