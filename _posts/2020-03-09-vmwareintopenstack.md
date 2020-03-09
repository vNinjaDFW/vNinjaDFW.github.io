---
layout: post
title:  VMware Integrated OpenStack
date:   2020-03-09-vmwareintegratedopenstack
image:  vio_icon.jpg
tags:   [vExpert, vio, OpenStack]
---
In September of 2019, I was "deployed" to New York on a new engagement. While I was working on cleaning up the environment and implementing VMware best practices, I encounteredered VMware Integrated Openstack 3.1. If you're not familiar with VIO, it's a VMware service that automates the deployment and management of an Openstack cloud architecture by streamlining the integration process. There are many appliances that are deployed during the installation process including a pair of Controllers, DHCP Servers, Databases and Load Balancers. Most of the terminology used by VIO is an overlay of the native Openstack terms including Nova, Cinder, Glance, Neutron, Keystone and Horizon.

Here's a small table to help map VMware and OpenStack terminology.

VMware | OpenStack Terminology
------------ | -------------
Nova | Compute
Cinder | Storage
Glance | Templates
Neutron | Network
Horizon | Web Portal
KeyStone | Identity Service
Heat | Orchestration

Because of the version of vCenter and ESXi (6.0) that was being used, I knew that one of the things we would need to do to the environment was upgrade to 6.7. I had numerous roadblocks during the planning stages, inculding the old and unsupported version of VIO. Right off the bat, I had two options to suggest. First, upgrade in stages from 3.1 to 6.0. Alternatively, which was my recommendation based on my findings, was to evacuate the VIO environment and move the VMs to native VMware. After a few discussions and getting buy-in from the Customer, I wrote a script that would migrate powered-off VMs from VIO to native VMware.

If you find yourself in a similar position, reach out to me and I'll help walk you thru some of the steps and what needs to happen. There are some configuration changes in the script that will be needed but I can help you with that.

Head over to my Script repository to download it and many others.

Visit https://github.com/vNinjaDFW/Scripts and look for the VMware folder and then VM_Migrations. (MigrateVIO_VMs.ps1)