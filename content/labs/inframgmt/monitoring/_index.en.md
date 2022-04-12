+++
title = "Monitoring SAP"
date = 2022-03-14T14:13:05-03:00
weight = 5
chapter = false
pre = "<b></b>"
+++

### Azure Monitor for SAP

When you have critical applications and business processes relying on Azure resources, you'll want to monitor those resources for their availability, performance, and operation.

Azure Monitor for SAP Solutions is an Azure-native monitoring product for anyone running their SAP landscapes on Azure. With Azure Monitor for SAP Solutions, you can collect telemetry data from Azure infrastructure and databases in one central location and visually correlate the data for faster troubleshooting.

You can monitor different components of an SAP landscape, such as Azure virtual machines (VMs), high-availability cluster, SAP HANA database, SAP NetWeaver, and so on, by adding the corresponding provider for that component. 

![MON](/images/monitor-sample.png?height=300px)

One of the benefits of monitoring SAP on Azure is the integrated view of both Infrastructure metrics (like CPU, RAM and Disk) alongside HANA database metrics (like memory usage and memory growth), and Netweaver metrics like concurrent sessions and locks. With embedded Log Analytics and Workbooks it allow for using the monitoring data so you can:

- Create custom visualizations by editing the default Workbooks provided by Azure Monitor for SAP Solutions.
- Write custom queries.
- Create custom alerts by using Azure Log Analytics workspace.
- Take advantage of the flexible retention period in Azure Monitor Logs/Log Analytics.
- Connect monitoring data with your ticketing system.

This allows for a rapid response in case of an incident response as well as providing a simpler and more integrated way of having the whole SAP performance picture in a glance. 

This lab is based on the [Azure Monitor for SAP Quickstart](https://docs.microsoft.com/en-us/azure/virtual-machines/workloads/sap/azure-monitor-sap-quickstart) guide. 

### What we will build

{{< youtube SGfpUqr8cao >}}

### Estimated Time for this Lab

This lab is estimated to take between 20 and 30 minutes.

### Requirements

For this demo we will be using the following components from the Environment Setup: 

1. S/4HANA deployed from SAP CAL
2. Azure subscription