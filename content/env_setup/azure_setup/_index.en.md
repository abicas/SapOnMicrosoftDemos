+++
title = "Azure Setup for SAP CAL"
date = 2022-03-08T16:34:27-03:00
weight = 2
chapter = false
pre = "<b></b>"
+++

SAP has a platform called SAP Cloud Application Library (SAP CAL), designed to automatically deploys SAP software on cloud hyperscalers. 

In order to allow for SAP to deploy an S/4HANA environment in your Azure subscription, we need to setup permissions for it in your subscription.

This section will go thru the steps required to setup your subscription

### What you will need

1. An existing Azure subscription with enough credits for the labs
2. Administrator access on the subscription
3. A temporary text file to make note of the required information related to endpoints and keys 

{{% notice warning %}}
In order to be able to deploy on your subscription, permissions used here will be quite broad. Make sure you go thru cleanup section to remove it after the labs, to avoid incidental usage of those credentials for non-authorized access to your subscription. In production environments, you should go thru the SAP and Microsoft best practices and setup access with the minimum required permissions and controls. 
{{% /notice %}}

### Expected duration

This section is estimated to last no longer than 10 minutes
