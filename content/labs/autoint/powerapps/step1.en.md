+++
title = "SAP Custom Connector"
weight = 7
pre = "<b>1. </b>"
chapter = false
+++

In this step we will create a custom connector to SAP on [Power Apps](https://www.office.com/). Custom connectors are used when you have a specific data source for which you know how to handle the requests. In this example we will use a premade example for the SAP Gateway Demo System (configured on the setup phase, section 4 - in case you skipped this step, please stop and create your access to the SAP Gateway Demo). 

The steps required are: 

1. Go to [Office.com](https://www.office.com/). 
2. Click on the **9 dots Icon on the Top Left**
3. Select **Power Apps** (it can also be found under All Apps)
![Powerapp](/images/log00.png?height=300)
4. In Power Apps, expand Data and click on **Custom Connectors**. Select **New Connector** and pick the **Import from Github** option
![Powerapp](/images/log01.png?height=400)
5. Select **Custom**, branch **master** and Connector **SAP-ODATA-DEMO** 
![Powerapp](/images/log02.png?height=300)
6. Rename it to **SAPGWDEMO**, check the parameters and click on **Security**
![Powerapp](/images/log03.png?height=400)
7. Make sure we are using **Basic Authentication** and click **Definition**
![Powerapp](/images/log04.png?height=400)
8. This connector has already some preconfigured interfaces. Feel free to explore then to understand how it handles API calls and click on **Create Connector** to proceed. 
![Powerapp](/images/log05.png?height=400)

Now you should have a custom connector configured, allowing you to access SAP Gateway ODATA APIs thru your Power App. 
On the next section we will create an App to use this data. 