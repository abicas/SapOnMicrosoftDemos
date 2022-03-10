+++
title = "Create a Workflow"
date = 2022-03-10T14:52:21-03:00
weight = 6
chapter = false
pre = "<b>2. </b>"
+++

In this step we will create the Workflow  on [Azure Portal](https://portal.azure.com). 

1. Go to **Logic Apps** 
2. Click on your Logic App **SAPDemo**
3. Go to **Workflows** and **Add** a new one as the parameters below: 
![Logic App](/images/logicapp02.png)
4. Click on **Designer** and let's start building the Workflow! 
5. As the first operation, which starts the flow, we will pick **When a HTTP request is received**
![Logic App](/images/logicapp03.png)
6. In order to customize the payload we expect, let's **Use a sample payload to generate schema** 
    - Sample payload: `{"id": "0000000728"}`
![Logic App](/images/logicapp04.png)
7. This will generate a schema for the trigger
![Logic App](/images/logicapp05.png)
8. Now we will create our temp variable to hold the desired part of the SAP reponse. Add a new action and type "initialize" on the search box. Select **Initialize Variables**
![Logic App](/images/logicapp06.png)
9. In this step, we will create na empty array to store the data:
    - Name: **outputArray**
    - Type: **Array**
    - Value: **[]**
![Logic App](/images/logicapp07.png)
10. Next we will invoke BAPI method in SAP by adding a new Action (make sure you select **Azure** ) called **[BAPI] Call method in SAP**
![Logic App](/images/logicapp08.png)
11. Now we need to link this BAPI call with the On-premises Data Gateway we installed on Bastion Host. Click on **Change connection**
![Logic App](/images/logicapp09.png)
12. An now we provide the connection information required so Logic Apps can communicate with SAP:
    - Connection Name: **SAPS4CAL**
	- DataGateway: Select your Gateway, in this case SapDemoGW
	- Client: **100**
	- Auth: **Basic**
	- User: **BPINST**
	- Password: **Welcome1**
	- AS HOST: Public IP of your SAP HANA on SAP CAL (this IP will change if you shutdown SAP. You will have to follow the same procedure to manually update upon activation or resort to dynamic DNS)
	- AS SERVICE: **50000**
	- AS SYSTEM NUMBER: **00**
    - Accept other defaults and click **Create**
![Logic App](/images/logicapp10.png)
13. Logic App will test the connection and you should see the **Connected** status 
![Logic App](/images/logicapp11.png)
14. Now let's setup the BAPI method to be invoked
    - Business Object: **BUS2032:SalesOrder**
    - Method: **GETSTATUS:Display Sales Order:BAPI_SALESORDER_GETSTATUS**
    - Input: `<GETSTATUS xmlns="http://Microsoft.LobServices.Sap/2007/03/Rfc/"><SALESDOCUMENT>xxx</SALESDOCUMENT></GETSTATUS>`
    - Replace xxx on the above Input with a Dynamic Content **id** extracted from the trigger on step 7. Make sure there are no spaces between SALESDOCUMENT
![Logic App](/images/logicapp12.png)
![Logic App](/images/logicapp14.png)
15. Add a new **Parse JSON** action
![Logic App](/images/logicapp15.png)
16. In content use **JsonResponse** that will be passed by BAPI
![Logic App](/images/logicapp16.png)
17. As we did on the initial step, select **Use sample payload to generate schema** and use the following JSON sample
`{"STATUSINFO":[{"DOC_NUMBER":"0000000728","DOC_DATE":"2018-11-06","PURCH_NO":"xcwer","PRC_STAT_H":"C","DLV_STAT_H":"C","REQ_DATE_H":"2018-11-06","DLV_BLOCK":"","ITM_NUMBER":"000010","MATERIAL":"CM-FL-V01","SHORT_TEXT":"Forklift","REQ_DATE":"2018-11-21","REQ_QTY":1.0,"CUM_CF_QTY":1.0,"SALES_UNIT":"ST","NET_VALUE":8000.0,"CURRENCY":"USD","NET_PRICE":8000.0,"COND_P_UNT":1.0,"COND_UNIT":"ST","DLV_STAT_I":"C","DELIV_NUMB":"","DELIV_ITEM":"000000","DELIV_DATE":"","DLV_QTY":0.0,"REF_QTY":0.0,"S_UNIT_ISO":"PCE","CD_UNT_ISO":"PCE","CURR_ISO":"USD","MATERIAL_EXTERNAL":"","MATERIAL_GUID":"","MATERIAL_VERSION":"","PO_ITM_NO":"","CREATION_DATE":"","CREATION_TIME":"00:00:00","S_UNIT_DLV":"","DLV_UNIT_ISO":"","REA_FOR_RE":"70","PURCH_NO_C":"xcwer","MATERIAL_LONG":"CM-FL-V01"},{"DOC_NUMBER":"0000000728","DOC_DATE":"2018-11-06","PURCH_NO":"xcwer","PRC_STAT_H":"C","DLV_STAT_H":"C","REQ_DATE_H":"2018-11-06","DLV_BLOCK":"","ITM_NUMBER":"000020","MATERIAL":"CM-FL-V00","SHORT_TEXT":"Forklift","REQ_DATE":"2018-11-06","REQ_QTY":7.0,"CUM_CF_QTY":0.0,"SALES_UNIT":"ST","NET_VALUE":58800.0,"CURRENCY":"USD","NET_PRICE":8400.0,"COND_P_UNT":1.0,"COND_UNIT":"ST","DLV_STAT_I":"C","DELIV_NUMB":"","DELIV_ITEM":"000000","DELIV_DATE":"","DLV_QTY":0.0,"REF_QTY":0.0,"S_UNIT_ISO":"PCE","CD_UNT_ISO":"PCE","CURR_ISO":"USD","MATERIAL_EXTERNAL":"","MATERIAL_GUID":"","MATERIAL_VERSION":"","PO_ITM_NO":"","CREATION_DATE":"","CREATION_TIME":"00:00:00","S_UNIT_DLV":"","DLV_UNIT_ISO":"","REA_FOR_RE":"70","PURCH_NO_C":"xcwer","MATERIAL_LONG":"CM-FL-V00"}]}`
![Logic App](/images/logicapp17.png)
18. SAP Sales Order can have multiple Line Items, so we have to iterate in them. Add na **For Each** action and as parameter, **STATUSINFO** from Parse JSON previous action.
![Logic App](/images/logicapp18.png)
19. Inside the For Each loop add a **Compose** action. It will allow for us to pick desired fields for each line and build a JSON that suits our needs.
![Logic App](/images/logicapp19.png)
20. Build the desired JSON using the sample JSON below and replacing fields enclosed by `<>` using **Dynamic Inputs** as inputs (make sure you keep the commas)
`{ 
  "Order": <DOC_NUMBER>,
  "Date": <DOC_DATE>,
  "Item": <MATERIAL>,
  "Description": <SHORT_TEXT>,
  "Quantity": <REQ_QTY>,
  "Price": <NET_PRICE>
}
`
![Logic App](/images/logicapp20.png)
21. Inside the For Each loop, after Compose, add na action **Append to array variable**. Select **outputArray** previously initialized as empty and for Value **Outputs** from Compose action
![Logic App](/images/logicapp21.png)
22. Once For Each runs and populates outputArray with the desired data, we will convert it to an HTML table. Add a **Create HTML table** Action and use the **outputArray** as the data for the table. 
![Logic App](/images/logicapp22.png)
23. Finally, we will add an action **Send an email** from **Office 365 Outlook**. You may need to connect Logic Apps with Office 365, by clicking on **Change connection** as did previously for SAP. 
![Logic App](/images/logicapp23.png)
24. Let's now build the email template that will be used on every invocation
    - To: **Destination email** 
    - Subject: **Details for order <ID>** (replace with dynamic content)
    - Body: as picture below 
![Logic App](/images/logicapp24.png)
25. As the API response we will add a **Response** action and return
    - Status Code: **200**
    - Body: **JsonResponse** from Dynamic inputs
![Logic App](/images/logicapp25.png)
26. Don't forget to click **SAVE** !!!! ;) 
![Logic App](/images/logicapp26.png)


If everything wen't fine, we are ready to test the lab we just built, with NO CODE at all ! 


















