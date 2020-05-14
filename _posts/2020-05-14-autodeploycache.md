---
layout: post
title:  Autodeploy [Entry Is Too Large To Be Added]
date:   2020-05-14-autodeploycache
image:  autodeploy.png
tags:   [vExpert, vCenter, VMUG]
---
After another vCenter 6.0 to vCenter 6.7 migration, I had to setup the Auto Deploy Software Depots with the needed Image Profile. As expected, I was able to add one, two, three and even a fourth repo with an Image Profile. When I went to add the fifth, I received an error "Entry is too large to be added to cache, remove any unused depots".

Since this was a new setup, I knew that I didn't have the option of removing any usused depots, so I had to find a way to increase the cache size. As I began digging into the vCSA cli options, I documented what I did to fix this. My environment is an embedded 6.7u3g with ELM to a duplicate environment in another city.

```powershell
less /etc/vmware-imagebuilder/sca-config/imagebuilder-config.props

vmomiPort=8098
cacheSize_GB=2
httpPort=8099
loglevel=INFO
```

As you can see, the cacheSize_GB is setup to 2 by default. I decided to double this using this command to edit the file. If you don't know how to use vi, there are plenty of articles that can help you.

```powershell
vi /etc/vmware-imagebuilder/sca-config/imagebuilder-config.props
less /etc/vmware-imagebuilder/sca-config/imagebuilder-config.props

vmomiPort=8098
cacheSize_GB=4
httpPort=8099
loglevel=INFO
```

Once I confirmed that the cacheSize_GB was now set to 4, I restarted the Image Builder and Auto Deploy services from the vCSA command line. There is an easy way to do this from the VAMI, but I was already ssh'd into the vCSA so I did it that way.

```powershell
service-control --restart vmware-imagebuilder
service-control --restart vmware-rbd-watchdog
```

I was then able to go back to the vCenter and import the remaining two Image Profiles that I needed!
