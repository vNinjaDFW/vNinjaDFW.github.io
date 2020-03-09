---
layout: post
title:  Add VMs To Inventory
date:   2020-03-09
image:  vm_icon.png
tags:   [vCenter, SRM, script]
---
A few years ago while performing a manual DR test, we ran into an issue with the storage. We had VMware SRM 6.x at the time, but we were testing something out with the Storage team due to some SRM cleanup issues. The storage team created a LUN snapshot and presented it as RO to the DR site. After I added those LUNs to the Hosts, I had to find a way to get all of the VMs registered in vCenter. The problem was that I had almost 50 VMs to register, and I didin't want to browse the LUN, goto the VM folder, and register each VMX file manually.

As I always do, I decided to create a script to do this for me. The reason I decided to do this was because of the number of the VMs to be registerd, and I didn't know how many times we would have to clean up and do this process again.

You can also register a virtual machine from a command line in an ESXi host:
1. Log in as root to the ESXi host with an SSH client.
2. Run the command:
    # vim-cmd solo/registervm /vmfs/volumes/datastore_name/VM_directory/VM_name.vmx

Head over to my Script repository to download it and many others.

Visit https://github.com/vNinjaDFW/Scripts and look for the VMware folder. (Add_All_VMX_To_Inventory_From_Datastore.ps1)