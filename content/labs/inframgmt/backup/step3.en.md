+++
title = "Run a Restore"
date = 2022-03-15T15:55:06-03:00
weight = 8
chapter = false
pre = "<b>3. </b>"
+++

Let's change some data and then run a restore for a point-in-time previous to the change. 

This section will show the steps required for that to be accomplished:

#### Changing some data

1. Go to the Bastion Host, and open the SAP GUI. Login with BPINST/Welcome1 default user. 
![bkp3](/images/re01.png)
2. On SAP GUI, go to TCODE MM02 to change a material. 
![bkp3](/images/re02.png)
3. For **Material** we will choose the **CM-FL-V00** a Forklift. Click on the Checkmark.
![bkp3](/images/re03.png)
4. For **Plant** we will choose the **1710** a Forklift. Click on the Checkmark.
![bkp3](/images/re04.png)
5. Change the description from **Forklift** to something else. Click on **SAVE**
![bkp3](/images/re05.png)

With the data changed, we now go to restore the database HDB to the previous state.

#### Restoring the Database

1. Go to **Backup items** and select **SAP HANA on Azure VM**
![bkp1](/images/ba15.png)
2. Right+Click the ellipsis for HDB and select **Restore**
![bkp3](/images/re06.png)
3. There will be 3 restore modes 
- Alternate Location - Restore to another HANA database on another host
- Overwrite DB - Restore on top of existing database
- Restore as Files - Restore to files on filesystem for manual recovery
- Select **Overwrite DB** and click on **Select**
![bkp3](/images/re07.png?height=250px)
4. Let's pick 15-20 minutes prior to the time of change. In the example the change was 10:15, so we are selecting 9:59 as the point-in-time. 
![bkp3](/images/re08.png?height=250px)
5. make sure the Restore Point is right and click **OK**
![bkp3](/images/re09.png?height=250px)
6. It will trigger  a deployment. 
![bkp3](/images/re10.png?height=100px)
7. To monitor the jobs, click on **Backup jobs** and you will see restore job. It should be **In Progress** for now. It should take roughly the same it took for backup. In this example 30 minutes. 
![bkp1](/images/re11.png)
8. In the meantime, if you check HANA Studio on BAstion host you will see HDB offline, being restored. REstore will take the database offline, restore it, and bring it back online. 
![bkp1](/images/re12.png)
9. After 30 minutes, the jobs is showing up as completed on the Azure Portal. 
![bkp1](/images/re13.png)

Now let's check for the data restored

#### Checking SAP status

1. Go to the Bastion Host and check HANA Studio for HDB being open. Double click for details. 
![bkp1](/images/re14.png)
2. Open SAP GUI. Login with BPINST/Welcome1 default user. 
![bkp3](/images/re01.png)
2. On SAP GUI, go to TCODE MM02 to change a material. 
![bkp3](/images/re02.png)
3. For **Material** we will choose the **CM-FL-V00** a Forklift. Click on the Checkmark.
![bkp3](/images/re03.png)
4. For **Plant** we will choose the **1710** a Forklift. Click on the Checkmark.
![bkp3](/images/re04.png)
5. Description should be back to **Forklift** as it was before the change we did. 
![bkp3](/images/re15.png)

Congratulations, you have completed the Azure Backup for HANA Section !!!!