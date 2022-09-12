---
layout: post
title:  Configure NSX-T Manager Backup
date:   2022-09-12-nsxtbackup
image:  nsxtlogo.png
tags:   [nsx,linux]
---
<h5>Procedure</h5>

1. From a browser, log in with admin privileges to the NSX Manager.

2. Select System > Backup & Restore.

3. Click Edit under the SFTP Server label to configure your SFTP server. 
   The steps in [Deploy Oracle Autonomous Linux VM](../ocilinux) can help you deploy a Linux VM in Oracle Cloud and configure SFTP.

4. Enter the IP address or FQDN of the backup file server.

5. The protocol text box is already filled in. SFTP is the only supported protocol.

6. Change the default port if necessary. The default port is 22.

7. In the Directory Path text box, enter the absolute directory path where the backups will be stored.

8. Enter the user name and password required to log in to the backup file server.

9. You can leave the SSH Fingerprint blank and accept or reject the fingerprint provided by the server after you click Save in a later step.

10. Enter a passphrase.

11. Click Save.

![]({{site.baseurl}}/img/nsxtbackupscreen.png)

12. Click Start Backup

![]({{site.baseurl}}/img/nsxtstartbackup.png)

You should see a successful backup!

![]({{site.baseurl}}/img/nsxtbackupsuccess.png)
