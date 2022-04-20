+++
title = "Building the Flow"
weight = 9
pre = "<b>3. </b>"
chapter = false
+++

In this step we will create the automation required to create products automatically on SAP via ODATA. 

The steps required are: 

1. Go to [Office.com](https://www.office.com/). 
2. Click on the **9 dots Icon on the Top Left**
3. Select **Power Apps** (it can also be found under All Apps)
![Powerapp](/images/log00.png?height=300)
4. Go to **Flows**. Select **New flow** and pick the **Instant cloud flow** option.
![auto0](/images/auto1-1.png?height=400)
5. Select the flow properties: 
- Name: **Excel2SAPGateway** 
- Trigger: **Manually trigger a flow** 
- Click **Create** 
![auto0](/images/auto1-2.png?height=400)
6. On the newly created flow, click on the **New Step** button to add a new step. 
![auto0](/images/auto1-3.png?height=100)
7. Filter by **Excel Online**, pick **Excel Online (Business)** and in Actions **List rows present in a table** (make sure you pick the Business version so it works with your Ofice365)
![auto0](/images/auto1-4.png?height=400)
8. Fill the parameters for the Excel file to be used as input: 
- Location: **OnceDrive for Business** 
- Document library: **OneDrive**
- File: Navigate to **/Excel2SAP/NewProductList.xlsx** 
- Table:  **NEWPRODUCTS** 
- Click on **New Step**
![auto0](/images/auto1-5.png?height=400)
9. Let's get the SAP credentials for the SAP gateway. Go to **Custom** and pick the **SAPGWDEMO** connector created on step #1.
![auto0](/images/auto1-7.png?height=400)
10. Under Actions, pick **Get product**
![auto0](/images/auto1-8.png?height=400)
11. In the Get product Action, fill the required fields: 
- id: **HT-1002** (must be an existing product under SAP Fiori ES5 Demo System)
- x-csrf-token: **fetch** (we will query and store the token for access later on)
![auto0](/images/auto1-9.png?height=400)
12. Now we are ready to scan the Excel file and line by line act upon the data. Add a new step, under **Control** called **Apply to each**. 
![auto0](/images/auto1-10.png?height=400)
13. Pick **value** from Dynamic content, under **List rows present in a table**. Add a new action. 
![auto0](/images/auto1-11.png?height=400)
14. Under **Custom**, pick **SAPGWDEMO** connector (inside the Apply to each loop)
![auto0](/images/auto1-12.png?height=400)
15. Pick the **Add product** action
![auto0](/images/auto1-13.png?height=400)
16. Fill the **x-csrf-token** with the Dynamic content from **Get product** 
![auto0](/images/auto1-14.png?height=400)
17. Fill **x-ms-cookie-header** with the **Expression** below, and click **OK**: 
``replace(outputs('Get_product')['headers']['Set-Cookie'],',',';')``
![auto0](/images/auto1-15.png?height=400)
18. Fill the remaining parameters with the values: 
- ProductID: Dynamic Content **Product ID** from List rows present in a table
- Type Code: **Product** (fixed value)
- Category: Dynamic Content **Product ID** from List rows present in a table
- Name: Dynamic Content **Product ID** from List rows present in a table
- SupplierID: **0100000046** (fixed value)
- Product Tax Code: **1** (fixed value)
- Currency Code: **United States Dollar** (fixed value)
- Price: Dynamic Content **Price(USD)** from List rows present in a table
- Description: Dynamic Content **Description** from List rows present in a table
- Unit of Measure: **each** (fixed value)
![auto0](/images/auto1-16.png?height=400)
19. Our flow is ready ! Click **SAVE** 
![auto0](/images/auto1-17.png?height=400)

Now you should have it all setup to test the Power Automate flow. 

On the next section we will execute the test and see the data on SAP. 