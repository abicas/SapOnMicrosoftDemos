+++
chapter = false
pre = "<b></b>"
title = "Azure Automation Start/Stop"
weight = 10
+++

### Azure Automation

Automation is needed in three broad areas of cloud operations:

- Deploy and manage - Deliver repeatable and consistent infrastructure as code.
- Response - Create event-based automation to diagnose and resolve issues.
- Orchestrate - Orchestrate and integrate your automation with other Azure or third party services and products.

Azure Automation delivers a cloud-based automation, operating system updates, and configuration service that supports consistent management across your Azure and non-Azure environments. It includes process automation, configuration management, update management, shared capabilities, and heterogeneous features.

![startstop](/images/startstop-sample.png?height=500px)

#### Process Automation
Process Automation in Azure Automation allows you to automate frequent, time-consuming, and error-prone management tasks. This service helps you focus on work that adds business value. By reducing errors and boosting efficiency, it also helps to lower your operational costs. The process automation operating environment is detailed in Runbook execution in Azure Automation.

Process automation supports the integration of Azure services and other third party systems required in deploying, configuring, and managing your end-to-end processes. The service allows you to author graphical, PowerShell and Python runbooks. To run runbooks directly on the Windows or Linux machine or against resources in the on-premises or other cloud environment to manage those local resources, you can deploy a Hybrid Runbook Worker to the machine.

Webhooks let you fulfill requests and ensure continuous delivery and operations by triggering automation from Azure Logic Apps, Azure Function, ITSM product or service, DevOps, and monitoring systems.

#### Common scenarios
Azure Automation supports management throughout the lifecycle of your infrastructure and applications. Common scenarios include:

- Schedule tasks - stop VMs or services at night and turn on during the day, weekly or monthly recurring maintenance workflows.
- Build and deploy resources - Deploy virtual machines across a hybrid environment using runbooks and Azure Resource Manager templates. Integrate into development tools, such as Jenkins and Azure DevOps.
- Periodic maintenance - to execute tasks that need to be performed at set timed intervals like purging stale or old data, or reindex a SQL database.
- Respond to alerts - Orchestrate a response when cost-based, system-based, service-based, and/or resource utilization alerts are generated.
- Hybrid automation - Manage or automate on-premises servers and services like SQL Server, Active Directory, SharePoint Server, etc.
- Azure resource lifecycle management - for IaaS and PaaS services.
- Resource provisioning and deprovisioning.
- Add correct tags, locks, NSGs, UDRs per business rules.
- Start-stop resources to save cost.
- Azure Site Recovery - orchestrate pre/post scripts defined in a Site Recovery DR workflow.
- Azure Virtual Desktop - orchestrate scaling of VMs or start/stop VMs based on utilization.
- Configure VMs - Assess and configure Windows and Linux machines with configurations for the infrastructure and application.
- Retrieve inventory - Get a complete inventory of deployed resources for targeting, reporting, and compliance.
- Find changes - Identify and isolate machine changes that can cause misconfiguration and improve operational compliance. Remediate or escalate them to management systems.

### What we will build

{{< youtube p6lYWcSEbfk >}}

### Estimated Time for this Lab

This lab is estimated to take between 90 and 120 minutes, mostly due to the time it takes for SAP to come up and shutdown gracefully.  

### Requirements

For this demo we will be using the following components from the Environment Setup: 

1. S/4HANA deployed from SAP CAL
2. Azure subscription   