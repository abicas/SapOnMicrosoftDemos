+++
title = "Power Automate Flow"
date = 2022-03-10T11:58:35-03:00
weight = 7
chapter = false
pre = "<b> </b>"
+++

### Power Automate

Power Automate is a service that helps you create automated workflows between your favorite apps and services to synchronize files, get notifications, collect data, and more.

Here are a few examples of what you can do with Power Automate.

- Automate business processes
- Send automatic reminders for past due tasks
- Move business data between systems on a schedule
- Connect to more than 500 data sources or any publicly available API
- You can even automate tasks on your local computer like computing data in Excel.

Just think about time saved once you automate repetitive manual tasks simply by recording mouse clicks, keystrokes and copy paste steps from your desktop! Power Automate is all about automation.

What skills do you need to have? Anyone from a basic business user to an IT professional can create automated processes using Power Automate's no-code/low-code platform.
![auto1](/images/auto-flow.png?height=500px)
Here you can see some [templates of what can be built](https://powerautomate.microsoft.com/en-us/templates/) as well as [Videos with demos around Power Automate](https://www.youtube.com/channel/UCG98S4lL7nwlN8dxSF322bA)

Power Automate provides an [extensive connector list](https://powerautomate.microsoft.com/en-us/connectors/) so you can automate tasks using triggers and actions from multiple platforms, including SAP. 
![auto1](/images/auto-connectors.png?height=400px)

### What we will build

In this lab we will build an automated flow (manually executed) that reads the contents of an Excel file stored on OneDrive and line by line creates new products on SAP by leveraging SAP Gateway ODATA interfaces.

You can see a sample of the lab below: 

{{< youtube xmtEac7Hw8s >}}

### Estimated Time for this Lab

This lab is estimated to take between 30 minutes. 

### Requirements

For this demo we will be using the following components from the Environment Setup: 

1. SAP Gateway Demo System
2. Azure subscription

