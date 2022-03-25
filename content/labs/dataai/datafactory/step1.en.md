+++
title = "Environment Preparation"
date = 2022-03-25T10:32:20-03:00
weight = 5
chapter = false
pre = "<b>1. </b>"
+++
Before we start extracting data from SAP, we need to create a repository to hold the extracted data. 

In this example we will be using Azure Data Factory to extract the data and store it in a Blob Storage of a Datalake.

This section will show the steps required to prepare the environment for that:

1. Log on to the [Azure Portal](https://portal.azure.com) and look for **Storage Accounts**
![monitoring1](/images/adf01.png?height=250px) 
2. Create a new Storage Account and provide the required information. Select the same region that SAP was deployed:
- Resource Group: **SAP_ADF** (create new RG)
- Storage Account Name: **sapadfXXXX** (must be unique on Azure, change XXXX by any set of 4 numbers) 
- Region: **East US** 
- Redundancy: **LRS** 
![monitoring1](/images/adf02.png?height=550px) 
3. On the newly created storage account, select **Containers** on the left pane and click on **+ Container** 
![monitoring1](/images/adf03.png?height=450px)
4. Name it **cntsapadf** and accept the default security of **Private**, once we don't want to expose business data to the internet. 
![monitoring1](/images/adf04.png?height=250px)

With those 4 steps we have created a repository to store the data. 

Let's create the Azure Data Factory instance now:
1. Log on to the [Azure Portal](https://portal.azure.com) and look for **Data factories**
![monitoring1](/images/adf05.png?height=350px) 
2. Create a new Data factory and provide the required information. Select the same region that SAP was deployed:
- Resource Group: **SAP_ADF**
- Name: **sapadfXXXX** (change XXXX by any set of 4 numbers) 
- Region: **East US** 
![monitoring1](/images/adf06.png?height=550px) 
3. Click **Next** or select the tab **Git configuration** and check **Configure Git later** once we will not be storing our pipelines in a repository in this example. After this, click **Create**
![monitoring1](/images/adf07.png?height=350px)

Now we will configure the **Integration Runtime** on our Bastion Host to have access to the SAP data: 
1. On the Data Factory overview page, click on **Open Azure Data Factory Studio**
![monitoring1](/images/adf08.png?height=350px) 
2. On the new tab that will open, create a **New Pipeline** 
![monitoring1](/images/adf09.png?height=250px) 
3. Name it **adfsap_pipeline** on the right tab that will open: 
![monitoring1](/images/adf10.png?height=450px) 
4. Click on the Toolbox icon on the left pane, then click on **Integration runtimes** and click on **New**. Select the **Self Hosted** option
![monitoring1](/images/adf11.png?height=400px) 
5. On the Integration runtime setup step, select **Self Hosted** again
![monitoring1](/images/adf12.png?height=350px)
6. And name it **SAPIntegrationRuntime**; click **Create**
![monitoring1](/images/adf13.png?height=450px)
7. Once we are not performing those action on the Bastion host itself, we will choose **Option 2: Manual Setup**. 
- Copy the **Key 1** Authentication Key that will be used on the runtime installation to some scratch area.
- Right click and **Copy the URL** from the **Step 1** (we will use it to download the software on the bastion host)
![monitoring1](/images/adf14.png?height=450px)
8. Go to the **Bastion Host via RDP and download** the latest version, using the URL provided in the step #7:
![monitoring1](/images/adf15.png?height=450px)
9. Install the downloaded software: 
![monitoring1](/images/adf16.png?height=350px)
10. On the setup phase, paste the **Authentication Key** from step #7, and click **Register**:
![monitoring1](/images/adf17.png?height=350px)
11. For this example, we will **Enable remote access from intranet** and click **Next**:
![monitoring1](/images/adf18.png?height=350px)
12. The Integration Runtime will contact the Data FActory using the Authentication Key provided and register itself. Click on **Launch Configuration Manager** and confirm that everything was OK:
![monitoring1](/images/adf19.png?height=350px)
![monitoring1](/images/adf20.png?height=350px)
13. All set on the Bastion Host, we will go back to the **Azure Portal**. Let's make sure the Integration runtime is showing up on the Data Factory. Click on **Refresh** button and it should show the newly registered SAPIntegrationRuntime:
![monitoring1](/images/adf22.png?height=350px)


Now, finally, we are ready to start extracting data from SAP! 

**The next 2 steps will be similar, divided by data provider**. 
