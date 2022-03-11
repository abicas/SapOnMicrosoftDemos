+++
title = "Creating our Chatbot"
date = 2022-03-10T17:25:38-03:00
weight = 5
chapter = false
pre = "<b>1. </b>"
+++
In this section we will create our Chatbot on Microsoft Power Platform. 

Go to [Office 365](https://office.com), authenticate and select **Power Apps**.
![VA](/images/va01.png?height=350px)

On Power Apps, expand **Chatbots**, select **Create** and click on the **Basic conversational bot** button.
![VA](/images/va02.png?height=450px)

Fill the information to create the bot: 
- Name: **SAP Bot**
- Language: **Deisred language** (examples in Brazilian Portuguese with translation)
- Environment: **US**
![VA](/images/va03.png?height=350px)

Once the bot is created, go to **Topics** and click on **New Topic**
![VA](/images/va04.png?height=250px)

Let's rename the newly created topic from Untitled to **PO Details** (en-US) / **Detalhes do Pedido** (pt-BR)
![VA](/images/va05.png?height=150px)

The bot needs know which phrases trigger this topic, so we will add some examples of questions users may pose to accomplish what they need: 
- en-US
    - I need details for a PO
    - I want PO details
    - I need to know line items of a purchase order
    - Inform the products in a purchase order
- pt-BR
    - Quero detalhes de uma ordem de compra
    - Preciso detalhes de um pedido
    - Quero saber os detalhes de uma PO
    - Informar produtos em um pedido
![VA](/images/va06b.png?height=200px) 

Let's add a new step, acknowledging the intent and asking the PO number to be queried, and another one asking the PO Number: 
- Message - Acknowledge
    - en-US
        - Ok. If I understood it correctly you with to know the line items of a Purchase Order (PO). I will need some extra info for that. 
    - pt-BR    
        - Ok, entendi que você precisa de uma lista dos items de uma Ordem de Compra (PO). Para isso vou precisar do número do pedido. 
- Question
    - en-US
        - Can you inform the PO number? (exactly 10 chars - leading zeroes)
    - pt-BR
        - Você pdoeria informar o número do pedido? (exatamente 10 caracteres - zeros a esquerda)
    - Parameters: 
        - Identify: **User's Entire Response** 
        - Variable Name: **PONumber** 
        - Type: **Text** (SAP compares strings so that is why we have leading zeroes and exactly 10 chars)
        - Usage: **Bot** (it allows us to use this info for further questions)
![VA](/images/va07.png?height=350px) 

Again, let's acknowledge the user input and add an action to query SAP. 
- Message - Acknowledge
    - en-US
        - Thank you! Searching for order "xxx" details ... 
    - pt-BR
        - Obrigado! Pesquisando a ordem "xxx"para você ...
    - IMPORTANT: replace xxx with **bot.PONumber** from dynamic values, like example below
- Add Action: 
    -  Add a **Call an Action** and click on **Create a flow**
![VA](/images/va08.png?height=350px) 

Now on the Flow we will: 
- Rename the Flow to **GetSAPOrderItems** 
- Define an Input variable called **PONumber** (type **Text**) inside the flow. Later on we will map this to the Bot.PONumber parameter. 
- We will show a table on the bot's answer. For this we will add an **Initialize Variable**, call it **OutputTable** (Type **String**) and add the following markdown content (don't forget to add new line at the end) that will be rendered as a table. 
```PYTHON
| Date | Item | Description | Quantity | Price | 
|-----------|:-----------:|:-----------:|:-----------:|-----------:| 
  
```
![VA](/images/va09.png?height=350px) 

Next we will invoke SAP BAPI method: 
- Add a **Call SAP function** step
- Set the required parameters: 
    - AS Host: **SAP HANA public IP**
    - Client: **100**
    - AS System Number: **00**
    - SAP Function Name: **BAPI_SALESORDER_GETSTATUS** 
    - SALESDOCUMENT: **PONumber** variable from dynamic values
![VA](/images/va10.png?height=450px) 

Let's now teach the Flow how to interpret SAP's response: 
- Add a **Parse JSON** action
- Generate Schema based on the JSON sample below by clicking on **Generate from Sample** and pasting it.
- Once the Schema is generated, define Content parameter as  **STATUSINFO** from Dynamic Values
```JSON
[
    {
      "DOC_NUMBER": "0000000728",
      "DOC_DATE": "2018-11-06",
      "PURCH_NO": "xcwer",
      "PRC_STAT_H": "C",
      "DLV_STAT_H": "C",
      "REQ_DATE_H": "2018-11-06",
      "DLV_BLOCK": "",
      "ITM_NUMBER": "000010",
      "MATERIAL": "CM-FL-V01",
      "SHORT_TEXT": "Forklift",
      "REQ_DATE": "2018-11-21",
      "REQ_QTY": "1.000",
      "CUM_CF_QTY": "1.000",
      "SALES_UNIT": "ST",
      "NET_VALUE": "8000.00",
      "CURRENCY": "USD",
      "NET_PRICE": "8000.00",
      "COND_P_UNT": "1",
      "COND_UNIT": "ST",
      "DLV_STAT_I": "C",
      "DELIV_NUMB": "",
      "DELIV_ITEM": "000000",
      "DELIV_DATE": "0000-00-00",
      "DLV_QTY": "0.000",
      "REF_QTY": "0.000",
      "S_UNIT_ISO": "PCE",
      "CD_UNT_ISO": "PCE",
      "CURR_ISO": "USD",
      "MATERIAL_EXTERNAL": "",
      "MATERIAL_GUID": "",
      "MATERIAL_VERSION": "",
      "PO_ITM_NO": "",
      "CREATION_DATE": "0000-00-00",
      "CREATION_TIME": "00:00:00",
      "S_UNIT_DLV": "",
      "DLV_UNIT_ISO": "",
      "REA_FOR_RE": "70",
      "PURCH_NO_C": "xcwer",
      "MATERIAL_LONG": "CM-FL-V01"
    },
    {
      "DOC_NUMBER": "0000000728",
      "DOC_DATE": "2018-11-06",
      "PURCH_NO": "xcwer",
      "PRC_STAT_H": "C",
      "DLV_STAT_H": "C",
      "REQ_DATE_H": "2018-11-06",
      "DLV_BLOCK": "",
      "ITM_NUMBER": "000020",
      "MATERIAL": "CM-FL-V00",
      "SHORT_TEXT": "Forklift",
      "REQ_DATE": "2018-11-06",
      "REQ_QTY": "7.000",
      "CUM_CF_QTY": "0.000",
      "SALES_UNIT": "ST",
      "NET_VALUE": "58800.00",
      "CURRENCY": "USD",
      "NET_PRICE": "8400.00",
      "COND_P_UNT": "1",
      "COND_UNIT": "ST",
      "DLV_STAT_I": "C",
      "DELIV_NUMB": "",
      "DELIV_ITEM": "000000",
      "DELIV_DATE": "0000-00-00",
      "DLV_QTY": "0.000",
      "REF_QTY": "0.000",
      "S_UNIT_ISO": "PCE",
      "CD_UNT_ISO": "PCE",
      "CURR_ISO": "USD",
      "MATERIAL_EXTERNAL": "",
      "MATERIAL_GUID": "",
      "MATERIAL_VERSION": "",
      "PO_ITM_NO": "",
      "CREATION_DATE": "0000-00-00",
      "CREATION_TIME": "00:00:00",
      "S_UNIT_DLV": "",
      "DLV_UNIT_ISO": "",
      "REA_FOR_RE": "70",
      "PURCH_NO_C": "xcwer",
      "MATERIAL_LONG": "CM-FL-V00"
    }
  ]
```
![VA](/images/va11.png?height=450px) 

As you can see, the response is an array, so we have to use **Apply to Each** action, based on the **Body** dynamic output of **Parse JSON** 
Inside the For Each loop, we will be appending the lines one by one to the outputTable varibale which had only the header so far. 
For each item in the array it will add a new line. We will add an **Append to string variable** action and use "|" to separate the dynamic values. 

IMPORTANT: Remember to include **opening and closing "|"** and **Add a NEW LINE** in the end
- Dynamic values used to build the line are: DOC_DATE, MATERIAL, SHORT_TEXT, REQ_QTY, NET_PRICE
![VA](/images/va12.png?height=450px) 

The last step on the Flow is to return the **OutputTable** variable back to the bot.
Add a **Return value to Power Virtual Agents** action after the For Each (not inside it) and create a variable called **outputTable** (Type **String**) which will have the dynamic value **OutputTable**
![VA](/images/va13.png?height=250px) 

Save the Flow and let's go back to the bot's topic itself. 

Now we should be able to see the newly created Flow **GetSAPOrderItens** when adding the **Call an action**
![VA](/images/va14.png?height=250px) 

Here we will link the bot's variables to the Flow ones. 
Map **PONumber** to **bot.PONumber**. It should autmatically get the outputTable variable from the flow. 
![VA](/images/va15.png?height=250px) 

Now we will show the outputTable variable (string) as part of the message. Add the text and use the **outputTable** dynamic value in the content. Bot will render it as table on Teams later on. 
- en-US
    - Here are the order details **outputTable** 
- pt-BR
    - Aqui estão os detalhes do pedido **outputTable** 
![VA](/images/va16.png?height=250px) 

Finally, add an **End** action and **SAVE** 





