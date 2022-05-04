+++
title = "HANA Demo DB Setup "
weight = 7
pre = "<b>1. </b>"
chapter = false
+++

Before we start generating insights from SAP HANA, we need to import a demo content provided by SAP called [SHINE](https://github.com/SAP-samples/hana-shine). 
In this step we will import the package, run the demo app and populate the database with demo data. We will also install Power BI Desktop app so we can start working with the SAP data in the next sections. 

#### Loading Sample data model (SHINE)
The steps required are: 
1. Go to the Bastion host. 
2. Download the **HCO_DEMOCONTENT** from [SAP SHINE GitHub Release page](https://github.com/SAP-samples/hana-shine/releases)
![prepbi](/images/prepbi09.png)

3. On the Bastion Host, open Hana Studio. 
4. Click File -> **Import**
![prepbi](/images/prepbi10.png)
5. Select the package type. Under **SAP HANA CONTENT** select **Delivery Unit** and click Next
![prepbi](/images/prepbi11.png)
6. Select the HDB Database and click Next
![prepbi](/images/prepbi12.png)
7. Click on Client, Browse, select the downlaoded file and click Finish
![prepbi](/images/prepbi13.png)
8. Wait until the import job completes successfully.
![prepbi](/images/prepbi14.png)
9. Now, let's add permissions to the user SAPHANADB. On Hana Studio, open **HDB**, open **Security**, open **Users** and select **SAPHANADB**. Click on the **Plus sign** and search for the role **sap.hana.demo**. Select **sap.hana.democontent.epm.roles::Admin** and click **OK**. 
![prepbi](/images/prepbi15.png)
10. Make sure the role has been selected and click the **Execute** green button on the top right. 
![prepbi](/images/prepbi16.png)
11. Let's test the XS app and populate the database. On the bastion host, go to [https://vhcals4hcs.dummy.nodomain:44301/sap/hana/democontent/epm](https://vhcals4hcs.dummy.nodomain:44301/sap/hana/democontent/epm) and click **Check Prerequiisites** 
![prepbi](/images/prepbi17.png)
12. Click on the **Generate Time data** and **Create Synonyms** and wait for the green checkmark. 
![prepbi](/images/prebi18.png)


#### Power BI desktop setup

Now the HANA database has the data model and the mock data, we need to install Power BI desktop so we can start building ! 

1. Go to the Bastion Host and **Download** [Power BI Desktop](https://www.microsoft.com/en-us/download/details.aspx?id=58494)
2. Proceed with the default installation process of the app. 
3. Make sure you have followed the steps described on the **Environment Setup section** on the **MICROSOFT ON-PREMISES DATA GATEWAY INSTALLATION** section so we can communicate via the gateway. 
4. Open the Power BI Desktop app and clear the initial splash screens. Click on **File** 
![pbisetup](/images/pbi10.png)
5. Go to **Options and Settings** and click on **Options** 
![pbisetup](/images/pbi11.png)
6. Select **Direct Query** and check the **Treat SAP HANA as a relational database** 
![pbisetup](/images/pbi12.png)

Alright we are ready to start working with Power BI and data. 

On the next two sections we will use two scenarios with PowerBI and Native HANA integrations: 
- Analyzing data directly from SAP HANA published objects (#2)
- Analyzing data from custom queries with mutiple datasources including SAP HANA (#3)

Choose your desired path (or both) and let's go !