+++
title = "Power Virtual Agent"
date = 2022-03-10T11:58:35-03:00
weight = 5
chapter = false
pre = "<b> </b>"
+++

### Power Virtual Agent

Microsoft Power Virtual Agents lets you create powerful chatbots that can answer questions posed by your customers, other employees, or visitors to your website or service.

These bots can be created easily without the need for data scientists or developers. Some of the ways that Power Virtual Agents bots have been used include:

- Sales help and support issues
- Product or Purchase Order informations
- Employee health and vacation benefits
- Common employee questions for businesses, products, processes

All this integrated with live SAP data, allowing customers to access the information they need, on a simple, common, practical platform they are used to, avoiding the burden of context switching between multiples apps to accomplish a task. 

![PVA](/images/pva-sample.png?height=500px)

Power Virtual Agents is available as both a standalone web app, and as a discrete app within Microsoft Teams.

### What we will build

In this lab we will build an chatbot that answers Sales Order details, using Power Virtual Agents and publishing the bot to Microsoft Teams. 

Whenever this bot is invoked, it triggers a a flow that will call an SAP BAPI based on user inputs process the response, build an HTML table and send it back to the chatbot. 

You can see a sample of the lab below: 

{{< youtube I9FuhBlQgpo >}}

### Estimated Time for this Lab

This lab is estimated to take between 30 and 60 minutes. 

### Requirements

For this demo we will be using the following components from the Environment Setup: 

1. S/4HANA deployed from SAP CAL
2. On-premises data gateway installed and configured 
3. Azure subscription