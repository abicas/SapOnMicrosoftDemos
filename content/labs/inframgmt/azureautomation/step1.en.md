+++
title = "Setup Azure Automation for SAP"
date = 2022-03-15T15:55:06-03:00
weight = 6
chapter = false
pre = "<b>1. </b>"
+++

In order to have Azure Automation gracefully managing SAP Worklaods, we need to setup the Azure Automate and import some runbooks. 

This section will show the steps required for that to be accomplished:

#### Azure Automation Setup

1. Log on to the [Azure Portal](https://portal.azure.com) and go to **Automation Accounts** 
![SS1](/images/startstop-1.png?height=150px) 
2. Create an Automation Account with the following parameters: 
- Resource Group: Pick the SAPCAL-XXXXXXXX created by SAP CAL so we can cleanup properly. 
- Account Name: **SAPAutomationAcc** 
- Region: **East US** (same as SAP)
- Click **Review and Create** and then in **Create**
![SS1](/images/startstop-2.png?height=350px) 
3. Go to the newly create SAPAutomationAcc
![SS1](/images/startstop-3.png?height=350px) 

#### Importing Modules
Let's add a Module to run PowerShell commands with SAP. 

4. On the left pane click on **Modules** and **Add Module** 
![SS1](/images/startstop-4.png?height=350px) 
5. Click on **Browse from gallery** 
![SS1](/images/startstop-5.png?height=350px) 
6. Search for **SAPAzure** and pick **SAPAzurePowershellModules** 
![SS1](/images/startstop-6.png?height=150px) 
7. Click on **Select** 
![SS1](/images/startstop-7.png?height=350px) 
8. Pick the Runtime **5.1** and click **Import** 
![SS1](/images/startstop-8.png?height=350px) 

#### Importing Runbooks 
Now we will import the template runbooks required for automating SAP. There is an extensive list but we will only use the ones required for the SAP CAL deployment model. Other deployment modules mey need additional modules. Please see [the complete documentation](https://github.com/Azure/SAP-on-Azure-Scripts-and-Utilities/tree/main/Start-Stop-Automation/Automation-Backend) for more information.

{{% notice info %}}
The procedure below will be executed for 8 Runbooks: 
- Stop-SAPSystem
- Start-SAPSystem
- List-SAPSystemInstances
- Stop-SAPHANA
- Start-SAPHANA
- List-SAPHANAInstance
- Start-SAPApplicationServer
- Stop-SAPApplicationServer

Please at the end of this procedure, repeat the sequence for the remaining runbooks 
{{% /notice %}}

9. On the left pane click on **Runbooks** and **Import a Runbook** 
![SS1](/images/startstop-9.png?height=350px) 
10. Go to **Browse from gallery** 
![SS1](/images/startstop-10.png?height=350px) 
11. Search for the Runbook Name from the list above and pick **Source: Powershell Gallery**. In this example we are searching for **Stop-SAPSystem** but you will do the same procedure for all the 8 Runbooks required. 
![SS1](/images/startstop-11.png?height=250px) 
12. Click **Select** 
![SS1](/images/startstop-12.png?height=350px) 
13. Use the **same name**from the template, pick runtime **5.1** and click **Import** 
![SS1](/images/startstop-13.png?height=350px) 
14. Click on **Publish** and **Yes** 
![SS1](/images/startstop-14.png?height=350px) 
15. Go back to **SAPAutomationAcc** by clicking on the top link
![SS1](/images/startstop-15.png?height=350px) 
16. Repeat the process for all the other runbooks. 
![SS1](/images/startstop-16.png?height=350px) 

At the end your **SAPAutomationAcc** screen should look like this, with all the 8 runbooks imported: 
![SS1](/images/startstop-17.png?height=350px) 

#### Adding Execution Permissions (Run As Accounts)

In order to start and stop SAP, Azure Automation needs to log in as root to those VMs. Let's give it the permissions for this: 

4. Go back to the **SAPAutomationAcc**, scroll down the left panel and select **Run as accounts**. Click on **Azure Run As Accounts** 
![SS1](/images/startstop-20.png?height=400px) 
5. Wait until the green checkmark is added to the option. This will expire in 365 days. 
![SS1](/images/startstop-21.png?height=400px) 

Congratulations, you have configured the Azure Automation and imported the required runbooks.Now let's move to the next section and add Tags to our VMs so the script can identify the VMs properly. 

