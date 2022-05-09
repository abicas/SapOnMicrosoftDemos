+++
title = "Azure Backup for HANA"
date = 2022-03-10T11:55:46-03:00
weight = 5
chapter = false
pre = "<b> </b>"
+++

### Azure Backup for HANA 

SAP HANA databases are critical workloads that require a low recovery-point objective (RPO) and long-term retention. You can back up SAP HANA databases running on Azure virtual machines (VMs) by using Azure Backup.

Azure Backup is Azure's native backup solution, which is [BackInt certified by SAP](https://sapblobs.blob.core.windows.net/csd-live/azure-backup-backint-11-certificate-e34b4b20-5ea5-11ec-987d-359059e8f619). This offering aligns with Azure Backup’s mantra of zero-infrastructure backups, eliminating the need to deploy and manage backup infrastructure. 

Benefits:
- 15-minute Recovery Point Objective (RPO): Recovery of critical data of up to 15 minutes is possible.
- One-click, point-in-time restores: Easy to restore production data on SAP HANA databases to alternate servers. Chaining of backups and catalogs to perform restores is all managed by Azure behind the scenes.
- Long-term retention: For rigorous compliance and audit needs, you can retain your backups for years, based on the retention duration, beyond which the recovery points will be pruned automatically by the built-in lifecycle management capability.
- Backup Management from Azure: Use Azure Backup’s management and monitoring capabilities for improved management experience.

![bkpforhana](/images/bkpforhana-sample.png?height=500px)

Sample Backup flow: 
1. The scheduled backups are managed by crontab entries created on the HANA VM by Azure Backup, while the on-demand backups are directly triggered by the Azure Backup service.

2. Once SAP HANA Backup Engine/Backint receives the backup request, it prepares the SAP HANA database for a backup by creating a save point, and moving data to underlying storage volumes.

3. Backint then executes the read operation from the underlying data volumes – the index server and XS engine for the Tenant database and name server for the SYSTEMDB. Premium SSD disks can provide optimal I/O throughput for the backup streaming operation. 

4. To stream the backup data, Backint creates up to three pipes, which directly write to Azure Backup’s Recovery Services vault.

5. Azure Backup attempts to achieve speeds up to 420 MB/sec for non-log backups and up to 100 MB/sec for log backups. 

6. Detailed logs are written to the backup.log and backint.log files on the SAP HANA instance.

7. Once the backup streaming is complete, the catalog is streamed to the Recovery Services vault. If both the backup (full/differential/incremental/log) and the catalog for this backup are successfully streamed and saved into the Recovery Services vault, Azure Backup considers the backup operation is successful.

### What we will build

In this lab we will configure and run a backup directly from HANA (backint) to Azure Backup and then restore the database. 

The video below shows a backup running, data being changed, a restore and then the data back to its original state after the restore. 

{{< youtube jnnijsS8CKY >}}

### Estimated Time for this Lab

This lab is estimated to take between 90 and 120 minutes, mostly due to backup and restores processes. 

### Requirements

For this demo we will be using the following components from the Environment Setup: 

1. S/4HANA deployed from SAP CAL
2. Azure subscription   