+++
title = "Environment Setup"
date = 2022-03-08T16:31:36-03:00
weight = 5
chapter = false
+++

Before we start building our labs we need to have provisioned a few resources: 
- An Azure subscription setup for SAP Cloud Appliance Library (SAP CAL)
- An existing S/4HANA environment or a trial deployed thru SAP CAL
- Installation of Microsoft Data Gateway components
- An account at the SAP Gateway Demo System for some integration examples

The following sections will guide you thru the steps to accomplish this and be ready to the labs. 

{{% notice info %}}
Some components used will depend on Trial licenses that expire after a given period of time. Before building production content on top of those labs, make sure you do this in a properly licensed enviroment to avoid losing your work.
{{% /notice %}}

{{% notice warning %}}
ATTENTION: Some VMs for SAP HANA used in this lab can become quite expensive if you let it running 24x7. Make sure you define shutdown timers and in the end of your labs, go thru the Environment Cleanup section to remove unecessary resources.
This lab is not responsible for costs related to its examples. 
{{% /notice %}}