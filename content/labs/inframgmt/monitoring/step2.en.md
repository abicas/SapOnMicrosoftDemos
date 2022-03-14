+++
title = "HANA Provider"
date = 2022-03-14T14:22:13-03:00
weight = 6
chapter = false
pre = "<b>2. </b>"
+++

Let's add a HANA Provider to collect metrics for us: 

1. On the Azure Monitor for SAP, go to **Providers**
![monitoring1](/images/am05.png?height=450px)
2. Click **Add**
![monitoring1](/images/am06.png?height=100px)
3. Let's fill the required data: 
- Type: **SAP HANA** 
- IP Address: **SAP HANA Private IP Address**
- Database tenant: **SYSTEMDB** 
- SQL Port: **30215** 
- Username: **SAPHANADB**
- Password: **Password defined during deploy of SAP CAL** 
![monitoring1](/images/am07.png?height=500px)
4. Wait for the Provider to be created and the data validated.
![monitoring1](/images/am08.png?height=100px)
5. It takes about 10-15 minutes for information to be initially available on Azure Monitor. Once this time has passed, go to **Monitoring -> SAP HANA** on the left blade. 
![monitoring1](/images/am09.png?height=200px)
6. Select the desired HANA instance (you can monitor several instances like DEV/QAS/PRD on so on...)
![monitoring1](/images/am10.png?height=300px)

An from here on, you should be able to see collected data directly from SAP HANA: 

Overview with peak CPU and RAM, HANA services status and licenses)
![monitoring1](/images/am11.png?height=500px)

Historic utilization data for CPU and Memory 
![monitoring1](/images/am12.png?height=500px)

Data size and growth 
![monitoring1](/images/am13.png?height=500px)

And more data like Backups and System Checks for Save Points and Delta Merges 
![monitoring1](/images/am14.png?height=400px)

Next step we will add operating system counter to the Azure Monitor for SAP.
