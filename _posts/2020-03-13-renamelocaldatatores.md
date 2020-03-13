---
layout: post
title:  Rename Local Datastores
date:   2020-03-13-renamelocaldatastores
image:  vm_icon.png
tags:   [PowerCLI]
---
Overnight, my Customer deployed 68 new ESXi Hosts in two Datacenters. That alone is an amazing accomplishment, but there are multitudes of things that have to happen from an Operations point of view. Even though we're using Host Profiles for most of the settings, renaming the local datastore is not available (at least not on ESXi 6.0). I did what I always do when I have a task that needs to be executed more than a few times....I wrote a script. The script will rename the local datastores of a cluster and move these datastores to a folder.

When you deploy a new ESXi Host by default, the local datastore is named "datastore1". If you deployed 34 new hosts in a single vCenter, it would look like:

- datastore1
- datastore1 (1)
- datastore1 (2)
- ...
- datastore1 (33)

As ugly as that looks, and it does, think about this operationally. If we left the datastores the way they are, there's not a FAST way to open the local datastore of a specific Host. I mean, sure you could goto the Host in question, and then goto the local storage. BUT, imagine if you could make it visually appealing and functionally better! The script below and in my repository, will name the local storage and move said datastores into a single Folder.

If you had a hostname of vNinja.isawesome.local and it had a local datastore of datastore1, using this script the local datastore would change to: local_storage_vNinja

The majority of my scripts are kept in my repository, but this is a fluid location. I am constantly putting my scripts up there for safe-keeping as well as to share with the vCommunity. As always, if you need something scripted that you don't see in there, reach out to me and I'll see if I can help.

Check out my [Scripts Repository][my-scripts] and look for Rename_Local_Datastores.ps1 in the VMware folder.

[my-scripts]: https://github.com/vNinjaDFW/Scripts/
