+++
title = "Remote Desktop Access"
date = 2022-03-09T09:55:28-03:00
weight = 6
chapter = false
pre = "<b>2. </b>"
+++

Let's connect to an RDP session on the Bastion Host. 

Use the Public IP for the Remote Desktop provided on the **Instance** tab. 

- Default User: **Administrator**
- Default Password: **The one used during the SAP deployment** 

Once connected you should see a screen similar to this. If the message says it is still under deployment, log off and wait a little bit longer. 
![Connect](/images/rdpacc01.png)

We will basically use 3 apps installed here:
- Web browser 
- SAP Logon (GUI)
- HANA Studio

The connection information for the SAP GUI is: 
- Client: **100**
- User: **BPINST**
- Password: **Welcome1**
- SID: **S4H**
![SAP GUI](/images/rdpacc02.png)


For SAP HANA Studio: 
- Host: **vhcalhdbdb** (local hosts file)
- Instance Number: **02**
- Multiple Containers - Tenant Database: **HDB** 
- Port: **30215**
- User: **SAPHANADB**
- Password: **The one used during the SAP deployment**

If not existant: 
1. Right click on the left pane and select **Add System**
![SAP GUI](/images/rdpacc03.png)
2. Fill the connection info
![SAP GUI](/images/rdpacc04.png?height=450px)
3. Fill the user and password
![SAP GUI](/images/rdpacc05.png?height=450px)

Once connection is created, double click on the connection on the left pane to see the HANA status: 
![SAP GUI](/images/rdpacc06.png)

Alright! SAP has been deployed, we are able to connect, and we are ready to start installing the Azure required components on the next section. 

