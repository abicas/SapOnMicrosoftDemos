+++
title = "Setup Azure Backup"
date = 2022-03-15T15:55:06-03:00
weight = 5
chapter = false
pre = "<b>1. </b>"
+++

In order to have Azure Backup backing up SAP HANA databases, we need to setup the Azure Backup as well as the HANA Database Server.

This section will show the steps required for that to be accomplished:

#### SAP HANA Setup

We need to connect to the SAP HANA Server and run a script that will prepare the database for Azure Backup. 

1. Log on to the [Azure Portal](https://portal.azure.com) and open a **Cloud Shell** (BASH)
![monitoring1](/images/ba00.png?height=100px) 
2. We need to SSH to the server, using the SAP provided certificate key (can be downloaded from SAP CAL again), previously uploaded to the CloudShell and having permission as 400). 
```bash
mod@Azure:~$ ssh -i <KEYNAME>.pem root@<HANA PUBLIC IP>
sid-hdb-s4h:~ # 
```
3. Then we will change the user to the HANA administrator **hdbadm**, store the database password in a secure storage, and return to root. 
```bash
sid-hdb-s4h:~ # sudo su - hdbadm
sid-hdb-s4h:HDB:hdbadm /usr/sap/HDB/HDB02 2> hdbuserstore set azure_key localhost:30213 SYSTEM '<YOUR SAP DEFINED PASSWORD>'
sid-hdb-s4h:HDB:hdbadm /usr/sap/HDB/HDB02 4> exit
logout
sid-hdb-s4h:~ # 
```
4. As **root**, we will download and run the setup script: 
```bash
sid-hdb-s4h:~ # wget https://go.microsoft.com/fwlink/?linkid=2173610 -O pre-script.sh
--2022-03-14 19:44:01--  https://go.microsoft.com/fwlink/?linkid=2173610
Resolving go.microsoft.com (go.microsoft.com)... 184.50.50.164, 2600:1408:c400:e82::2c1a, 2600:1408:c400:e80::2c1a
Connecting to go.microsoft.com (go.microsoft.com)|184.50.50.164|:443... connected.
HTTP request sent, awaiting response... 302 Moved Temporarily
Location: https://download.microsoft.com/download/B/2/E/B2E01EF8-C247-42A6-BCC7-E45B78F20C99/msawb-plugin-config-com-sap-hana.sh [following]
--2022-03-14 19:44:01--  https://download.microsoft.com/download/B/2/E/B2E01EF8-C247-42A6-BCC7-E45B78F20C99/msawb-plugin-config-com-sap-hana.sh
Resolving download.microsoft.com (download.microsoft.com)... 204.79.197.219
Connecting to download.microsoft.com (download.microsoft.com)|204.79.197.219|:443... connected.
HTTP request sent, awaiting response... 200 OK
Length: 87552 (86K) [application/octet-stream]
Saving to: ‘pre-script.sh’

sid-hdb-s4h:~ # chmod +x pre-script.sh
sid-hdb-s4h:~ # ./pre-script.sh --system-key azure_key 
[2022-03-14T19:45:08+00:00] [INFO] Checking if 'root'.
[2022-03-14T19:45:08+00:00] [PASS] Running as 'root'.
[2022-03-14T19:45:08+00:00] [INFO] Checking OS support.
[2022-03-14T19:45:08+00:00] [PASS] Found supported OS_NAME_VERSION = 'SLES-15.1'.
[2022-03-14T19:45:08+00:00] [INFO] Checking for free space in '/opt'.
[2022-03-14T19:45:08+00:00] [PASS] Found at least 2 GiB space on '/opt'.
[2022-03-14T19:45:08+00:00] [INFO] Checking HOSTNAMES.
[2022-03-14T19:45:08+00:00] [PASS] Found HOSTNAMES = [
[2022-03-14T19:45:08+00:00] [INFO]   '::1'
[2022-03-14T19:45:08+00:00] [INFO]   '10.0.0.166'
[2022-03-14T19:45:08+00:00] [INFO]   '127.0.0.1'
[2022-03-14T19:45:08+00:00] [INFO]   'fe80::222:48ff:fe2e:bde7'
...
[2022-03-15T17:56:40+00:00] [INFO] Checking login for BACKUP_KEY_USER = 'AZUREWLBACKUPHANAUSER'.
[2022-03-15T17:56:40+00:00] [PASS] Checked login.
[2022-03-15T17:56:40+00:00] [INFO] Granting privilege 'DATABASE ADMIN' to 'AZUREWLBACKUPHANAUSER'.
[2022-03-15T17:56:40+00:00] [PASS] Granted privilege.
[2022-03-15T17:56:40+00:00] [INFO] Granting privilege 'CATALOG READ' to 'AZUREWLBACKUPHANAUSER'.
[2022-03-15T17:56:40+00:00] [PASS] Granted privilege.
[2022-03-15T17:56:40+00:00] [INFO] Granting privilege 'INIFILE ADMIN' to 'AZUREWLBACKUPHANAUSER'.
[2022-03-15T17:56:40+00:00] [PASS] Granted privilege.
[2022-03-15T17:56:40+00:00] [INFO] Granting privilege 'BACKUP ADMIN' to 'AZUREWLBACKUPHANAUSER'.
[2022-03-15T17:56:40+00:00] [PASS] Granted privilege.
[2022-03-15T17:56:40+00:00] [INFO] Checking privilege 'CATALOG READ' on 'AZUREWLBACKUPHANAUSER'.
[2022-03-15T17:56:40+00:00] [PASS] Checked privilege.
[2022-03-15T17:56:40+00:00] [INFO] Checking privilege 'BACKUP ADMIN' on 'AZUREWLBACKUPHANAUSER'.
[2022-03-15T17:56:41+00:00] [PASS] Checked privilege.
[2022-03-15T17:56:41+00:00] [INFO] Checking privilege 'INIFILE ADMIN' on 'AZUREWLBACKUPHANAUSER'.
[2022-03-15T17:56:41+00:00] [PASS] Checked privilege.
[2022-03-15T17:56:41+00:00] [INFO] Checking privilege 'DATABASE ADMIN' on 'AZUREWLBACKUPHANAUSER'.
[2022-03-15T17:56:41+00:00] [PASS] Checked privilege.
[2022-03-15T17:56:41+00:00] [INFO] Adding user 'hdbadm' to group 'msawb'.
[2022-03-15T17:56:41+00:00] [PASS] Successfully added user.
[2022-03-15T17:56:41+00:00] [INFO] Writing to configuration.
[2022-03-15T17:56:41+00:00] [PASS] Writing complete.
[2022-03-15T17:56:41+00:00] [INFO] Writing to environment file.
[2022-03-15T17:56:41+00:00] [PASS] Writing complete.
[2022-03-15T17:56:41+00:00] [SUCC] Done.
```
At this point our HANA database is ready to be accessed by Azure backup and Backint (SAP Native Backup Agent) has been configured to send data to Azure. 

#### Azure Backup Setup 

1. Log on to the [Azure Portal](https://portal.azure.com) and open **Backup Center** 
![bkp1](/images/ba01.png?height=200px) 
2. On Backup Center we will create a **Vault** to store the backup data
![bkp1](/images/ba02.png?height=300px) 
3. For **Vault Type** select **Recovery Services Vault** 
![bkp1](/images/ba03.png?height=300px) 
4. Provide the Vault details: 
- Region: **East US** (Same as HANA database deployment)
![bkp1](/images/ba04.png?height=300px) 
5. Once the Vault is created, let's configure the **Backup** targets inside the Vault. 
![bkp1](/images/ba05.png?height=300px) 
6. Change the backup type to **SAP HANA on Azure VM** and click on Start Discovery. 
![bkp1](/images/ba06.png?height=300px) 
7. Select the HANA VM **<<instance name-SAP1** and click on **Discover DB** at the bottom of the page
![bkp1](/images/ba07.png?height=500px) 
8. Azure will start a deployment for the agent. Wait until you see the sucessfull message on Notifications
![bkp1](/images/ba07b.png?height=200px) 
9. Back to the Backup page, you should now have a **View Details** button. Click it so we can see the discovered Databases. 
![bkp1](/images/ba08.png?height=400px) 
10. Here you can see the discovered databases. Check the info and then close then window to go back to Backup
![bkp1](/images/ba09.png) 
11. Click on **Configure Backup**
![bkp1](/images/ba10.png) 
12. You can accept the default policy, select an existing one or Edit the current policy. 
![bkp1](/images/ba11.png)
13. In this lab we will create a simpler policy, called **DemoPolicy**. Click on **Edit** besides each item and configure it so it matches the example below.
![bkp1](/images/ba12.png)
14. Now let's add the discovered HANA databases. Click in **Add** and on the window that will open, select the DBs.
![bkp1](/images/ba13.png)
![bkp1](/images/ba14.png)
15. Click on **Enable Backup** once you have selected the HDB and SYSTEMDB databases. 
![bkp1](/images/ba14b.png?height=50px)
16. Now, let's make sure the items were correctly added and prepare for the first backup. Click on **Backup items** and then **SAP HANA in Azure VM**
![bkp1](/images/ba15.png?height=450px)
17. You should see a screen similar to this, with a **Warning (initial backup pending)** message
![bkp1](/images/ba16.png)

Congratulations, you have configured the HANA Backup using Azure Backup. Now let's move to the next section and run our first manual backup. 

