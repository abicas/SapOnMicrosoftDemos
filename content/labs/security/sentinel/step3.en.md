+++
title = "Deploy Sentinel SAP Agent"
date = 2022-03-14T14:22:13-03:00
weight = 9
chapter = false
pre = "<b>3. </b>"
+++

Now that the configuration steps are done, we are ready to deploy the agent that will gather SAP logs and dispatch them to Azure Sentinel.

{{% notice warning %}}
**SAP SOFTWARE DOWNLOAD**   

In order to be able to deploy the agent, we will need to download [SAP Netweaver SDK](https://aka.ms/sap-sdk-download) directly from SAP Downloads. Although it doesn't have a cost, it will require an SAP user with software download permissions.   

Please before continuing make sure you have an SAP user with proper permissions to download the required software or you won't be able to continue.
{{% /notice %}}


#### Downloading SAP Netweaver SDK

This download operation should be performed on your computer with your credentials to download SAP Software. 

1. Go to [SAP Support Lauchpad for downloading SAP Netweaver for SDK](https://aka.ms/sap-sdk-download). This link should bring you directly to the required download page. 
2. Login with your SAP S-User credentials 
![sso1](/images/sent9-1.png?height=350px) 
3. Click on the **SAP NW RFC SDK** file
![sso1](/images/sent9-2.png?height=350px) 
4. On the Download tab, select **LINUX ON X86_64 BIT** on the version and click on the **nwrfc*.zip** file. Download should start automatically. 
![sso1](/images/sent9-3.png?height=350px) 

#### Uploading the SAP Netweaver SDK

In this lab we will use the S/4HANA server itself to host the agent, so we can save on some costs. In a real world scenario you should deploy this agent in a separate VM for more security and isolation. 

1. Open a prompt/shell and go to the directory where you downloaded the SDK file. 
2. Copy the file to the root folder of the S/4HANA VM, using PuttySCP or SCP itself
```sh 
scp -i <YOUR PEM FILE>.pem nwrfc750P_11-70002752.zip root@<S/4HANA IP>:/root
```

#### Deploying the Agent

In this lab we will provide the SAP password for SENTINELUSR in a config file for simplicty and costs. In a real world scenario you should use an Azure Key Vault to safely store credentials as explained in this [article](https://learn.microsoft.com/en-us/azure/sentinel/sap/deploy-data-connector-agent-container?tabs=managed-identity)

1. Gather 2 values from the SAP Log Analytics workspace we created on step #1: Workspace ID and Primary Key. They will be required on the setup
![sso1](/images/sent5-2.png?height=450px) 
2. Open an SSH to the SAP S/4HANA server as root 
```sh
ssh -i <YOUR PEM FILE>.pem root@<S/4HANA IP>
```
3. Once logged in, download the installation script and set the execute permissions
```sh 
wget https://raw.githubusercontent.com/Azure/Azure-Sentinel/master/Solutions/SAP/sapcon-sentinel-kickstart.sh
chmod +x ./sapcon-sentinel-kickstart.sh
```
4. Run the script
```sh 
./sapcon-sentinel-kickstart.sh --keymode cfgf
```

So far your installation should be looking like this: 
![sso1](/images/sent5-1.png?height=550px) 

5. In the installation script: 
- Agree with the terms, by pressing <ENTER>
- Wait for it to download and install the required files and docker image
- Fill in the parameters:
    - ABAP Server Hostname: **<S/4HANA INTERNAL IP>**
    - System Number: **00**
    - SID: **S4H**
    - Client Number: **100**
    - SAP Username: **SENTINELUSR** 
    - SAP Password: **Microsoft01**
    - Log Analytics Workspace ID: **<WorkspaceID gathered in step 1>** 
    - Log Analytics Public Key: **<Primary key from step 1>** 

![sso1](/images/sent5-3.png?height=550px) 

6. As a final step, let's configure the docker agent container to restart automatically: 
```sh
docker update --restart unless-stopped sapcon-S4H
```
![sso1](/images/sent5-4.png) 

A few useful docker commands: 
- List running containers: docker ps -a
- View logs: docker logs sapcon-S4H
- View logs continuously: docker logs -f sapcon-S4H
- Stop the connector: docker stop sapcon-S4H
- Start the connector: docker start sapcon-S4H

7. Give a few minutes (5 should be enough) so logs start flowing and Sentinel is able to gather them and move over to the Azure Portal to see if everything is working. 
Go to Sentinel, select the Log Analytics we created, click on Data Connectors and hit refresh while filtering for SAP.   
If everything is working, you should see 1 agent connected and a green checkmark on the left side of Microsoft Sentinel for SAP.   
Head over to the connector page to see more details
![sso1](/images/sent5-5.png) 

8. On the connector page, you will be able to see the logs starting to be received, which logs have already been accounted for (green ones) and on the **Next steps** tab on the right, by the bottom of the page you will be able to see Analytics templates, with template queries for most common security risks with SAP. We will work with them on the next steps. 
![sso1](/images/sent5-6.png) 

Allright ! Now the agent is properly acessing SAP and pushing logs to Azure Sentinel. Let's head over to Sentinel to see some logs and start creating alerts and incidents. 
