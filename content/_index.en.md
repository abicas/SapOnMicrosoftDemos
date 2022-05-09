+++
title = "SAP on Microsoft"
date = 2022-03-08T16:31:36-03:00
weight = 1
chapter = false
+++
# Welcome to the ![SAP on Microsoft Labs](/images/SAPONMICROSOFTLABS-LOGO.png?height=250px)

This website is aimed to provide step-by-step guidance on how to prepare an SAP environment on Azure and demonstrate how can you integrate your SAP systems with Microsoft services and softwares. 

We know that for an environment like SAP, having a robust infrasctructure is a must-have but with Microsoft you can do much more! 

This website is divided in 3 main sections: 
- **Environment Setup**: Where we will go thru the steps required to run the labs on the next sections. Please don't skip.
- **SAP on Microsoft Labs**: Labs divided by category to create sample integrations between SAP and Microsoft
- **Environment Cleanup**: SAP can get quite expensive if let running 24x7. Here we will cleanup the environment created on Setup phase.

Each lab can be run individually from each other and are divided into sub-sections: 
- **Automation and Integration**
- **Data & AI**
- **Security**
- **Infrastructure and Management**

On each lab introduction page, you will be presented a quickl introduction about the Microsoft technology involved, a video with the lab final result, estimated time for completion, and requirements. 

### Navigating the site
Navigation between sections can be accessed on the left menu and each one will be divided into smaller chunks of steps. Also on the top right of your screen you have the next/back buttons to allow for easier navigation. 

![menu](/images/navigation.png?height=250px)

### Requirements

Before we start extending SAP, you need to have: 
- An Azure subscription with enough credits for running the environment
- An Office365 subscription with access to Power Platform

{{% notice info %}}
Some components used will depend on Trial licenses that expire after a given period of time. Before building production content on top of those labs, make sure you do this in a properly licensed enviroment to avoid losing your work.
{{% /notice %}}

{{% notice warning %}}
ATTENTION: Some VMs for SAP HANA used in this lab can become quite expensive if you let it running 24x7. Make sure you define shutdown timers and in the end of your labs, go thru the Environment Cleanup section to remove unecessary resources.
This lab is not responsible for costs related to its examples. 
{{% /notice %}}

### Running the Labs

It is **strongly recommended** that you go thru Environment Setup before anything else once the Labs assume the standards deployed in the previous section. Each lab will have an introductiory page with the requirements, in case you want to jump right into a specific lab. 

Also, **follow the steps in the order they were presented** otherwise you risk having to startover from scratch. 

### If you see something, say something 

This project is open source by nature and things can change pretty fast in the cloud environment. 
In case you see something wrong on the steps presented or something is not working as designed, feel free to contribute opening an issue or pushing a commit to [our Github project page](https://github.com/abicas/SapOnMicrosoftDemos).

### All set ! Let's go ! 

Are you ready to get started? 

Click on the right arrow for next page or navigate using the left side menu. 
