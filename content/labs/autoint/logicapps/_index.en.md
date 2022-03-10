+++
title = "Azure Logic Apps"
date = 2022-03-10T11:58:35-03:00
weight = 5
chapter = false
pre = "<b> </b>"
+++

### Azure Logic Apps 


### What we will build

In this lab we will build an API and receives a JSON payload with the Sales Order to be queries on SAP and sends the required information via Outlook using native SAP and Office 365 integrations. 

Whenever this API is used, it triggers a Logic App (built with no code) that will analyze the payload, run a BAPI on SAP, process the response, build an HTML table and send it by email alongside with the BAPI JSON. 

You can see a sample of the lab below: 

{{< youtube wqMKEuQEmIA >}}