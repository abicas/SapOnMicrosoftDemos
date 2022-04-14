+++
title = "Environment Cleanup"
date = 2022-03-19T09:19:24-03:00
weight = 9
chapter = true
pre = "<b> </b>"
+++

Now that you have done all the labs, it is important to cleanup deployed resources. 

Below we will see the steps required for this process: 

## SAP CAL Cleanup

This process will remove all resources deployed by SAP into your Azure Subscription. This is a destructive process and in case you need to recover this environment, you can redeploy from scratch until the end of the SAP CAL Trial. 

1. Sign in to the [SAP CAL](https://cal.sap.com/) and click on **Log On**. 
2. Go to **Instances**, click on the **ellipsis button** and select **Terminate**
![del](/images/delete01.png?height=300px)
3. Confirm the termination by clicking **OK**
![del](/images/delete02.png?height=100px)

{{% notice info %}}
This process can take up to 30 minutes. 
During the process the status will go from **Active** to **Terminating**. 
Once it is completed the status will change to **Terminated**
{{% /notice %}}

Wait until the termination is complete to proceed on the Azure part. 

## Azure Cleanup

This process will remove all resources under the deleted reesource groups of your Azure Subscription. This is a destructive process with no recovery possible besides redeploying. 

{{% notice warning %}}
Before proceeding, make sure SAP CAL resources have been removed and Instance status on SAP CAL is **TERMINATED** as per guidance above. 
{{% /notice %}}

4. Sign in to your Azure Account through the [Azure Portal](https://portal.azure.com)
5. Let's start by removing all the remaining resources deployed on the same SAP resource groups. Navigate to **Resource Groups**
![del](/images/delete03.png?height=150px)
6. Here you can see the existing resource groups. 
![del](/images/delete04.png?height=300px)
7. Click on the ones you want to delete (the ones created by SAP have SAPCAL in their names) and click on **Delete resource group**. On the panel on the right side, mark **Apply force delete** and write the name of the Resrouce Group to confirm. Click **Delete**. 
![del](/images/delete04b.png?height=150px)
**REPEAT this process to all resource groups named SAPCAL or that you want to remove** 

8. Let's remove the SAP CAL access from the Active Directory, thus removing its privileges to launch any new workloads on Azure. Go to **Azure Active Directory**
![del](/images/delete05.png?height=200px)
9. Go to **App registrations** and open the one you created for SAP CAL
![del](/images/delete06.png?height=300px)
10. Select **Delete**. Once completed SAP CAL credentials will be invalid. 
![del](/images/delete07.png?height=500px)


## SAP Gateway Demo System Cleanup

Although not required, because it doesn't impact in costs, you can opt to delete your SAP Gateway Demo Account. This process will remove the access and delete the account. In case you need to have access to it again, you will have to register again from scratch. 

1. Go to the [ES5 Login page](https://register.sapdevcenter.com/SUPSignForms/)
2. Click on the **Delet Account** button
![del](/images/delete08.png?height=500px)

## All set 

All the resources have been deleted if the procedures were sucessfull. 

Thank you for having followed thru the labs and we sincerely hope they were of value for you and your business! 

This project is open source by nature and things can change pretty fast in the cloud environment. 

In case you see something wrong on the steps presented, something is not working as designed, or you wanna give a feedback, feel free to contribute opening an issue or pushing a commit to [our Github project page](https://github.com/abicas/SapOnMicrosoftDemos).
