---
layout: post
title:  Configure VMware HCX Manager Backup
date:   2022-09-19-hcxbackup
image:  hcxlogo.png
tags:   [hcx,linux]
---
Previously, we learned how to [Deploy Oracle Autonomous Linux VM](../ocilinux) to deploy a Linux VM in Oracle Cloud and configure SFTP. If you do not have an SFTP server, I would recommend reading that.

<h5>Procedure</h5>
1. Log in to the appliance management interface: <https://hcx-ip-or-fqdn:9443>.

2. Navigate to Administration > Troubleshooting > Backup & Restore.

   ![]({{site.baseurl}}/img/hcxback1.png)

3. *(Optional)* Set up an FTP or SFTP server for uploading the backup file:
   a. Click the FTP server setting tab.
      ![]({{site.baseurl}}/img/hcxback2.png)
   b. Click Add.
   c. Enter the FTP or SFTP server information and click Save.

4. *(Optional)* Configure a backup schedule:
   a. Click the Scheduling tab.
   b. Click Add.
   c. Select the Backup Frequency.
   d. Enter the hour and minute of the backup.
   e. Click Save

5. Click the Backup and Restore tab.

6. Click Generate.
   *If a backup schedule is configured, the system creates the backup file at the scheduled time.*

7. For manual backups, save the backup file.
