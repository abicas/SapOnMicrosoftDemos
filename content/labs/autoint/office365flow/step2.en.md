+++
title = "Preparing OneDrive"
weight = 8
pre = "<b>2. </b>"
chapter = false
+++

In this step we will setup an One Drive folder to run our lab. 

The steps required are: 

1. Go to [Office.com](https://www.office.com/). 
2. Click on the **9 dots Icon on the Top Left**
3. Select **One Drive** (it can also be found under All Apps)
![auto0](/images/auto0-1.png?height=300)
4. Under **My Files**. Select **New** and pick the **Folder** option.
- Name: **Excel2SAP** 
![auto0](/images/auto0-2.png?height=400)
5. Download the [sample spreadsheet](/assets/NewProductList.xlsx). This is the product list we will automatically create into SAP. Open it and change the yellow cells following the template provided:
- Category: **Pick from the dropdown** 
- Name: ***XXX-9999** 
- Price: **0000-9999** 
- The other fields are automated with formulas, so no need to change them.   
![auto0](/images/auto0-4.png?height=400)
6. Save and upload the Excel file to the **Excel2SAP** folder
![auto0](/images/auto0-3.png?height=400)

Now you should have it all setup to build the Power Automate flow to insert this data into SAP via ODATA and SAP Gateway.
On the next section we will create a Flow to use this data. 