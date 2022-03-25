+++
title = "SAP TABLE Provider"
date = 2022-03-25T10:32:20-03:00
weight = 7
chapter = false
pre = "<b>3. </b>"
+++

Let's create a new pipeline and extract data to the Blob Storage: 

1. On the **Data Factory Studio**, click on the **Pencil icon** on the left, click the **Dataset Ellipsis** and select **New Dataset** 
![monitoring1](/images/adf45.png?height=150px) 
2. For the datastore, we will search for **SAP** and select **SAP Table**:
![monitoring1](/images/adf46.png?height=350px)
3. For the properties: 
- Name: **SapTable1**
- Create a **New** under **Linked Service**
![monitoring1](/images/adf25.png?height=350px)
4. Fill the required data for the linked service: 
- Name: **SapTable1**
- Integration Runtime: **SAPIntegrationRuntime**
- Server Name: **<<HANA IP>>**
- System Number: **00** 
- Client Id: **100** 
- Username: **BPINST**
- Password: **Welcome1** 
- Click on **Test connection** and if successful, click on **Apply**
![monitoring1](/images/adf47.png?height=550px)
5. Select the newly created **SapTable1** linked service, select Table **MATDOC** and click **OK**
![monitoring1](/images/adf48.png?height=450px)

We are now communicating with SAP via Netweaver. 

**Jump to STEP 4 on this LAB: Extracting data** 
(this is based on the values provided on the Step 3, but pipeline source data can be changed to match what the dataset we just set up)


