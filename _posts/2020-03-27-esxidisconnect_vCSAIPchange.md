---
layout: post
title:  ESXi Host Disconnects - vCenter IP Change
date:   2020-03-27-esxidisconnect_vCSAIPchange
image:  vm_icon.png
tags:   [vExpert, VMUG, vCenter]
---
After a recent vCenter 6.0 to vCenter 6.7 migration, I ran across an issue from previous years which reared it's ugly head. The Virtualization team had changed the vCenter IP (successfully) at some point in the past, but something wasn't completely done as a result. Even before the upgrade, I did noticed that some ESXi Hosts would not reconnect to vCenter automatically. When I would go and check that ESXi Host, I would see a message that it was being managed by 'x.x.x.x', which turned out was the **OLD** vCenter IP. This old IP was no longer responding to pings or DNS resolution. It was partly my fault for not investigation this further, but it came back to bite us post-vCenter upgrade.  

Post-vCenter upgrade to 6.7u3b, I immediately begin seeing vMotions and Alerts showing ESXi Hosts disconnecting and reconnecting. After connecting to the ESXi Host via ssh, I ran the command to check the vpxa.cfg file for the serverIp and serverPort information.

```powershell
grep -i server* /etc/vmware/vpxa/vpxa.cfg

/etc/vmware/vpxa/vpxa.cfg: <defaultClientPoolConnectionsPerServer>300</defaultClientPoolConnectionsPerServer>
/etc/vmware/vpxa/vpxa.cfg: <serverIp>1.2.3.4</serverIp>
/etc/vmware/vpxa/vpxa.cfg: <serverPort>902</serverPort>
```

From this command, I was able to determine that the serverPort was correct, but the serverIp was the **OLD** vCenter IP. I went to my Google skills and found [VMware's KB Article.](https://kb.vmware.com/s/article/1001493)

<h5>Method 1</h5>
1. Log in as root to the ESXi/ESX host with an SSH client. For more information, see Using Tech Support Mode in ESXi 4.1 and ESXi 5.x (1017910).
2. Open the /etc/opt/vmware/vpxa/vpxa.cfg file using a text editor and change the serverIp parameter to the new IP of the vCenter Server.

ESXi 5.x/6.0: The vpxa.cfg file is located at /etc/vmware/vpxa/vpxa.cfg.

3. Save your changes and exit.
4. Restart the management agents on the ESXi/ESX. For more information, see Restarting the Management agents on an ESX Server (1003490).
5. Restart the VMware VirtualCenter Server service. For more information, see Stopping, starting, or restarting the vCenter Server service (1003895).

<h5>Method 2</h5>
1. From the vSphere Client, right-click the ESXi/ESX host and click **Disconnect.**
2. From the vSphere Client, right-click the ESXi/ESX host and click **Reconnect.** If the IP is still not correct, go to step 3.
3. From the vSphere Client, right-click the ESXi/ESX host and click **Remove.**

**Caution**: After removing the host from vCenter Server, all the performance data for the virtual machines and the performance data for the host is lost.

4. Reinstall the VMware vCenter Server agent. For more information, see Verifying and reinstalling the correct version of VMware VirtualCenter Server agent (1003714).
5. Click **New > Add Host.**
6. Enter the information used for connecting to the host.

_Of course, if either one of these methods had fixed my issue, I wouldn't have anything to write about. It's always a great learning experience for me when it's **NOT** a simple fix. That's what it takes to continually grow and have a greater depth of knowledge._

1. Powered down the vCenter Server _(After obtaining a Change Window)_

2. Created a snapshot while the vCenter Server is in a powered off state for easy roll-back if need be. _(if this had an embedded PSC, we would need to power down all other external and embedded PSCs and snapshot them too, while all are powered off)_

3. Powered on the vCenter Server and allowed services to start

4. Stopped the vCenter Server vmware-vpxd service:
```powershell
service-control --stop vmware-vpxd
```
5. Log into the vCenter Server database 
```powershell
/opt/vmware/vpostgres/current/bin/psql -d VCDB -U postgres

6. Check the value stored in VPX_PARAMETER's "VirtualCenter.AutoManagedIPV4":
VCDB=# select * from vpx_parameter where name = 'VirtualCenter.AutoManagedIPV4';

7. Change this to the correct value, and check the value again:
VCDB=# update vpx_parameter set value = '2.4.6.8' where name = 'VirtualCenter.AutoManagedIPV4';
VCDB=# select * from vpx_parameter where name = 'VirtualCenter.AutoManagedIPV4';

8. Check the value for the "management_ip" for all hosts in the vpx_host table:
VCDB=# select management_ip,dns_name from vpx_host;

9. Change this value to "NULL" and check the value again:
VCDB=# update vpx_host set management_ip = NULL where management_ip IS NOT NULL;
VCDB=# select management_ip,dns_name from vpx_host;

10. Exit the database
VCDB=# \q

11. Start vCenter Server services
service-control --start vmware-vpxd

Once everything was confirmed correct, I went back and deleted the Snapshots. Alas, the **OLD** vCenter IP is **GONE** forever.