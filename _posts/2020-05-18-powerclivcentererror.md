---
layout: post
title:  PowerCLI vCenter Connection Error
date:   2020-05-18-powerclivcentererror
image:  
tags:   [vExpert, PowerCLI]
---
On a recent engagement with a customer, I upgraded one out of four vCenters from 6.0 to vCSA 6.7. I noticed an issue when trying to connect to this new vCSA with PowerCLI. The message I got was:

```powershell
Connect-VIServer : 5/18/2020 2:43:17 PM Connect-VIServer The underlying connection was closed: An unexpected error occurred on a send.
At line:1 char:1
+ Connect-VIServer vCenter69
+ ~~~~~~~~~~~~~~~~~~~~~~~~~~~~
+ CategoryInfo : NotSpecified: (:) [Connect-VIServer], ViError
+ FullyQualifiedErrorId : Client20_ConnectivityServiceImpl_Reconnect_WebException,VMware.VimAutomation.ViCore.Cmdlets.Commands.ConnectVIServer
```

A quick search on kb.vmware.com let me know that beginning with vSphere 6.7, only TLS 1.2 is enabled by default and TLS 1.0 and TLS 1.1 are disabled by default.

Due to the Customer's security constraints, enabling TSL 1.0 or TLS 1.1 was **NOT** an option. Another issue that presented itself was the Customer's change management process. Because we accessed PowerCLI thru a jumpbox in their Datacenter, we weren't able to upgrade PowerCLI to a newer version. You can see the command below on how to determine your PowerCLI version.

```powershell
PowerCLI C:\> Get-PowerCLIVersion

PowerCLI Version
----------------
VMware vSphere PowerCLI 6.3 Release 1 build 3737840
```

Being that I am very profecient with Powershell, I spent a few minutes looking into a way to initiate a TLS 1.2 connection before connecting to the vCenter. All you have to do is copy\paste the code below prior to initiating a connection. You can also put this code into any scripts you have running on a schedule if you cannot update your PowerCLI immediately.

```powershell
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
```

A connection attempt to your vCenter, should look like this:

```powershell
PowerCLI C:\> [Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12
PowerCLI C:\> Connect-VIServer vCenter69
```

Don't forget to check out my [Scripts Repository][my-scripts] for many helpful scripts.

[my-scripts]: https://github.com/vNinjaDFW/Scripts/