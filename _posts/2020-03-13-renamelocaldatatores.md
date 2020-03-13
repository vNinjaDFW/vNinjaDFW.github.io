---
layout: post
title:  Rename Local Datastores
date:   2020-03-13-renamelocaldatastores
image:  vm_icon.png
tags:   [PowerCLI]
---
Overnight, my Customer deployed 68 new ESXi Hosts in two Datacenters. That alone is an amazing accomplishment, but there are multitudes of things that have to happen from an Operations point of view. Even though we're using Host Profiles for most of the settings, renaming the local datastore is not available (at least not on ESXi 6.0). I did what I always do when I have a task that needs to be executed more than a few times....I wrote a script. The script will rename the local datastores of a cluster and move these datastores to a folder.

When you deploy a new ESXi Host by default, the local datastore is named "datastore1". If you deployed 34 new hosts in a single vCenter, it would look like:

datastore1
datastore1 (1)
datastore1 (2)
...
datastore1 (33)

As ugly as that looks, and it does, think about this operationally. If we left the datastores the way they are, there's not a FAST way to open the local datastore of a specific Host. I mean, sure you could goto the Host in question, and then goto the local storage. BUT, imagine if you could make it visually appealing and functionally better! The script below and in my repository, will name the local storage and move said datastores into a single Folder.

If you had a hostname of vNinja.isawesome.local and it had a local datastore of datastore1, using this script the local datastore would change to: local_storage_vNinja

This is just a snippet of the code and will not work without getting the full code from [Scripts Repository][my-scripts]. Look Rename_Local_Datastores.ps1 in the VMware folder for the full script.

Get-Cluster $cluster | Get-VMHost | % { $_ | Get-Datastore | ? {$_.name -match "^*datastore( \(\d+\))?$"} | Set-Datastore -Name "$prefix$($_.name.split(".")[0])"}

[my-scripts]: https://github.com/vNinjaDFW/Scripts/