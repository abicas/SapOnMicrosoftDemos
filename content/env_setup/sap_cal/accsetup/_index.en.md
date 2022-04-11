+++
title = "SAP CAL Account Setup"
date = 2022-03-09T09:55:28-03:00
weight = 5
chapter = false
pre = "<b>1. </b>"
+++
### Creating an SAP CAL account
First you need to create a free [SAP Cloud Appliance Library (CAL)](https://cal.sap.com/) account. 

Go to [https://cal.sap.com/](https://cal.sap.com/) and click on **Log On**. 

On the Login page, select **Register** and fill the required information. 

![Register](/images/sapcal01.png?height=250px)


### Granting Azure access
Once you got your approval e-mail from SAP, proceed to the SAP CAL website and Log On with your credentials, then follow the steps below: 

1. Go to **Accounts** and click on **Create Account**
![Accounts](/images/sapcal02.png?height=150px)
2. Give it a name, select Microsoft Azure and fill the data with the information gathered. 
![Accounts](/images/sapcal03.png?height=350px)
3. Click on **Test Connection** to make sure the parameters are valid.
![Test](/images/sapcal04.png?height=150px)

Alright, now we have the proper access to deploy a S/4HANA in your subscription. 

### Deploying SAP S/4HANA
SAP CAL allows for a 30 day Trial of the Solutions available, where SAP licenses are waived; only the cloud provider hosting fees apply. You can setup auto-shutdown and auto-terminate later on to make sure we keep costs low. 

In order to deploy a Trial S/4HANA in you subscription: 

1. Go to **Solutions**, pick the latest **SAP S/4HANA Fully-Activated Appliance** and click on **Create Instance**. 
![Solution](/images/sapcal05.png)
2. Select the newly created **Account**
![Solution](/images/sapcal07.png)
3. Read and Accept the License terms of the Trial
![Solution](/images/sapcal08.png)
4. Go to **Advanced Mode** so we can understand the parameters used on the deploy
![Solution](/images/sapcal09.png)
5. Select your account.
![Solution](/images/sapcal10.png)
6. Give your instance a name, description and validate the networking settings for the VNet. SAP will create a **Default SAP CAL Network** in case you have a new subscription. Select **Public Static IP address** so we can have remote access without the need for a VPN. 
![Solution](/images/sapcal11.png)
7. We won't be deploying Business Objects so on the next step, you can desselect this VM. Later on you can change the VM types on azure to cheaper, smaller or newer ones. Scroll down and check all the parameters, ports, disk sizes so you can familiarize with the solution. 
![Solution](/images/sapcal12.png)
8. Provide a password for SAP Admin access that will be customized during the deployment. There will be local pre-defined users and admin users with this password. 
For more details see the [Getting Started Guide](https://caldocs.hana.ondemand.com/caldocs/help/b8a9077c-f0f7-47bd-977c-70aa6a6a2aa7_Getting_Started_Guide_v12.pdf) for S/4HANA on SAP CAL with the default users and passwords. 
![Solution](/images/sapcal13.png)
9. Here we can adjust when the SAP will be available:
    - By Schedule - Scheduled start and shutdown 
    - Suspend on an Exact Date - Scheduled to be running for XX number of days and then shutdown. 
    - Manual - If you do not plan to use it everyday. When you activate you can setup a shutdown time in hours in case you forget.

    On the right side you can see the costs changing depending on the selection
![Solution](/images/sapcal14.png)
10. Click **Create** on the bottom of the page, review the data and go grab lunch (it should take 2-3 hours for the deployment to be complete).
![Solution](/images/sapcal15.png?height=150px)
11. You can monitor the progress of the deployment in the **Instances** tab. Wait for Activated status. 
![Solution](/images/sapcal16.png)

When the solution is deployed and activated, click on the instance name and check the top menu, where you can control the SAP landscape (suspend/terminate/activate) as well as the remote desktop IP address used as Bastion Host for managing the environment on Azure. 
![Solution](/images/sapcal17.png)

You can also access the **Getting Started Guide** under **Solution Info** tab as well make sure all the VMs are up and SAP was started properly and is communicating. 
![Solution](/images/sapcal18.png)

All done ! You have an SAP S/4HANA running in your susbcription ! 

On the next section let's see how we can access it and key users/passwords/parameters for conection that will be required later on. 









