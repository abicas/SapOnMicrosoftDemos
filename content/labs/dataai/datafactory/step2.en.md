+++
title = "HANA Provider"
date = 2022-03-25T10:32:20-03:00
weight = 6
chapter = false
pre = "<b>2. </b>"
+++

Let's create a new pipeline and extract data to the Blob Storage: 

1. On the **Data Factory Studio**, click on the **Pencil icon** on the left, click the **Dataset Ellipsis** and select **New Dataset** 
![monitoring1](/images/adf23.png?height=250px) 
2. For the datastore, we will search for **SAP** and select **SAP HANA**:
![monitoring1](/images/adf24.png?height=550px) 
3. For the properties: 
- Name: **SapHanaTable1**
- Create a **New** under **Linked Service**
![monitoring1](/images/adf25.png?height=350px)
4. Fill the required data for the linked service: 
- Name: **SapHana1**
- Integration Runtime: **SAPIntegrationRuntime**
- Server Name: **<<HANA IP>>:30215**
- Authentication Type: **Basic** 
- User name: **SAPHANADB** 
- Password: **Password defined on the CAL setup phase** 
- Click on **Test connection** and if successful, click on **Apply**
![monitoring1](/images/adf26.png?height=550px)
5. Select the newly created **SapHana1** linked service and click **OK** (we will not be selecting a table right now)
![monitoring1](/images/adf27.png?height=450px)

We are now communicating with SAP HANA. Let's see some data from Materials:

1. On the left pane, select the new Dataset created **SapHanaTable1** and for Table select **SAPHANADB.MATDOC**. Click Preview Data. (it may take a while for it to discover all the existing tables)
![monitoring1](/images/adf28.png?height=350px) 
2. You should see a sample of the table data. Take a look and close the box on the top right corner. 
![monitoring1](/images/adf29.png?height=450px) 

Alright, so by now we are communciating with SAP and have access to data. Let's create the pipeline to extract it to Blob.

**Jump to STEP 4 on this LAB: Extracting data** 
(Step 3 will be the same we just did but accessing SAP by the Netweaver layer)


