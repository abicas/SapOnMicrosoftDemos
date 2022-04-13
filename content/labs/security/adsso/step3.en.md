+++
title = "Testing SSO"
date = 2022-03-14T14:22:13-03:00
weight = 9
chapter = false
pre = "<b>3. </b>"
+++

Let's add a HANA Provider to collect metrics for us: 

#### Node Exporter Agent 
Before we start, we need to add an agent to the monitored VM. 


1. Go to the Azure Portal and open a Cloud Shell. In the examples we used BASH as the interpreter. 
![monitoring2](/images/am16.png?height=520px)
2. Now we will upload the key that SAP CAL generated on the deployment so we can log on to the Linux OS. Click on the **File Transfer icon**  and then **Upload**
![monitoring2](/images/am17.png?height=220px)
3. Select the key which will be a *.pem file, downladed from SAP CAL. If you do not remember or cannot find the file, go to [SAP CAL](https://cal.sap.com), select your instance, click on Download Key and download it again. 
![monitoring2](/images/am18.png?height=220px)
4. Let's add permissions to the .PEM file uploaded on the **Azure Cloud Shell** (in this example the key is called demosap.pem)
```bash
chmod 400 demosap.pem
```
5. With the key setup done, we can connect to the SAP HANA instance, usign the key as password for root: 
```bash
ssh -i demosap.pem root@<PUBLIC IP of HANA>
```
6. Let's download the agent. Go to [Prometheus Download Page](https://prometheus.io/download/) and copy the address for the latest **Node Exporter** for Linux
![monitoring2](/images/am19.png?height=220px)
7. Back to Azure Cloud Shell, we will download, extract the agent and copy it to /usr/bin. 
```bash
sid-hdb-s4h:~ # wget https://github.com/prometheus/node_exporter/releases/download/v1.3.1/node_exporter-1.3.1.linux-amd64.tar.gz
sid-hdb-s4h:~ # tar xvzf node_exporter-1.3.1.linux-amd64.tar.gz 
node_exporter-1.3.1.linux-amd64/
node_exporter-1.3.1.linux-amd64/LICENSE
node_exporter-1.3.1.linux-amd64/NOTICE
node_exporter-1.3.1.linux-amd64/node_exporter
sid-hdb-s4h:~ # cd node_exporter-1.3.1.linux-amd64/
sid-hdb-s4h:~/node_exporter-1.3.1.linux-amd64 # cp -pr node_exporter /usr/bin/
```
8. Let's test the agent by invoking it: 
```bash
sid-hdb-s4h:~ # node_exporter
ts=2022-03-14T18:58:29.764Z caller=node_exporter.go:182 level=info msg="Starting node_exporter" version="(version=1.3.1, branch=HEAD, revision=a2321e7b940ddcff26873612bccdf7cd4c42b6b6)"
ts=2022-03-14T18:58:29.764Z caller=node_exporter.go:183 level=info msg="Build context" build_context="(go=go1.17.3, user=root@243aafa5525c, date=20211205-11:09:49)"
ts=2022-03-14T18:58:29.764Z caller=node_exporter.go:185 level=warn msg="Node Exporter is running as root user. This exporter is designed to run as unpriviledged user, root is not required."
ts=2022-03-14T18:58:29.765Z caller=filesystem_common.go:111 level=info collector=filesystem msg="Parsed flag --collector.filesystem.mount-points-exclude" flag=^/(dev|proc|run/credentials/.+|sys|var/lib/docker/.+)($|/)
ts=2022-03-14T18:58:29.765Z caller=filesystem_common.go:113 level=info collector=filesystem msg="Parsed flag --collector.filesystem.fs-types-exclude" flag=^(autofs|binfmt_misc|bpf|cgroup2?|configfs|debugfs|devpts|devtmpfs|fusectl|hugetlbfs|iso9660|mqueue|nsfs|overlay|proc|procfs|pstore|rpc_pipefs|securityfs|selinuxfs|squashfs|sysfs|tracefs)$
ts=2022-03-14T18:58:29.765Z caller=node_exporter.go:108 level=info msg="Enabled collectors"
ts=2022-03-14T18:58:29.765Z caller=node_exporter.go:115 level=info collector=arp
ts=2022-03-14T18:58:29.765Z caller=node_exporter.go:115 level=info collector=bcache
```
9. On the **Bastion Host**, go to http://<<SAP HANA Private IP>>:9100/metrics
![monitoring2](/images/am20.png?height=420px)
10. Kill the node_exporter process with CTRL+C and start it in background
```bash
nohup node_exporter & 
```

The agent is installed and communicating internally on the vNET. Let's add the provider now

#### Linux Provider 

1. On the Azure Monitor for SAP, go to **Providers**
![monitoring1](/images/am05.png?height=450px)
2. Click **Add**
![monitoring1](/images/am06.png?height=100px)
3. Let's fill the required data: 
- Type: **OS Linux** 
- Endpoint: **http://internal_ip_address:9100/metrics**
![monitoring1](/images/am21.png?height=500px)
4. Wait until the provider is created and give it 10-15 minutes for data to start to flow. 
![monitoring1](/images/am22.png?height=100px)
5. Go to **Monitoring**, select **OS (Linux)**, and pick the host. 
![monitoring1](/images/am23.png?height=400px)

Congratulations, you just installed and finished the OS Linux Agent install. 

From here on, you should be able to see collected data directly from Linux: 

Overview with peak CPU and RAM, disk usage
![monitoring1](/images/am24.png?height=500px)

Historic CPU Monitoring
![monitoring1](/images/am25.png?height=500px)

Disk size and growth 
![monitoring1](/images/am26.png?height=500px)
