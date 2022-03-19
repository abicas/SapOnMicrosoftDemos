+++
title = "Run a Backup"
date = 2022-03-15T15:55:06-03:00
weight = 7
chapter = false
pre = "<b>2. </b>"
+++

With Azure Backups configured and communicating with SAP HANA database, let's execute a manual backup to test it. 

This section will show the steps required for that to be accomplished:

1. Log on to the [Azure Portal](https://portal.azure.com) and click on **Backup items** and then **SAP HANA in Azure VM**
![bkp1](/images/ba15.png?height=450px)
2. You should see a screen similar to this, with a **Warning (initial backup pending)** message. Right+Click the elipsis and select **Backup Now** for both HDB and SYSTEMDB.
![bkp1](/images/ba16.png)
3. To monitor the jobs, click on **Backup jobs** and you will see both submitted jobs. They should be **In Progress** for now. 
![bkp1](/images/ba17.png)
4. If you go to the Bastion Host and access **HANA Studio**, you can see the same jobs running from the SAP point of view. Double click **Backup** under HDB and see the right panel for details like estimated size, performance and status. 
![bkp1](/images/ba18.png)
5. Double clicking on **Backup** for SYSTEMDB will bring another tab called **Configuration**. Here we can see the parameters set by the setup script we ran in the previous section. Backint is SAP's backup agent for SAP, so having it configured means the agent is pushing data to Azure or other backup platform. 
![bkp1](/images/ba19.png)
6. Wait until the backup is finished. In the example environment, it took 30 minutes to backup 251GB of data @ 142MB/s. Performance may vary depending on server usage and other conditions. 
![bkp1](/images/ba20.png)
7. Same information can be seen on Azure Portal, by clicking on **Backup Jobs** and checking the status of the latest jobs: 
![bkp1](/images/ba21.png)
8. By selecting **Backup Items** and checking the status SAP HANA Backups we will see SYSTEM and HDB. Click on **View details** for HDB.  
![bkp1](/images/ba22.png)
9. It will show the available point-in-time restore and backups made. Point-in-time restoers are a combination of Backups + Logs, allowing for the agent to reconstruct the database at a given point-in-time (In the picture below, we left it running during the night. In your environment you will see the green bar growing with time, depending of the Log Backups)
![bkp1](/images/ba23.png)

Congratulations, we are now ready to test the restore option. LEt's move to the next section ! 