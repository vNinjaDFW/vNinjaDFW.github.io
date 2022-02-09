---
layout: post
title:  Bandwidth Testing between ESXi Hosts
date:   2022-02-09-esxibandwidthtesting
image:  
tags:   [esxi,iPerf,HCX]
---
I know I haven't written on my blog in over a year, but I'm hoping to reconnect with you on a more frequent basis. Now that I'm in a Pre-Sales role with Oracle, my primary functions are centered around [Oracle Cloud VMware Solution.](https://www.oracle.com/cloud/compute/vmware/)

I ran into an issue with Network performance and what we believed to be VMware HCX. In order to help pinpoint the bottleneck, I helped the Customer run some performance benchmarks. Many VMware admins might not know that iPerf comes pre-installed with ESXi since 6.5u2, which is the version I'm working with today.

I wasn't able to start iPerf in server mode without first making a copy of it, so here's the command to that.

```powershell
# Copy iPerf3 | Cannot start listener without this
cp /usr/lib/vmware/vsan/bin/iperf3 /usr/lib/vmware/vsan/bin/iperf3.copy
```

Next you'll want to disable the ESXi Firewall on both ESXi Hosts.
```powershell
# Run on Server & Client
esxcli network firewall set --enabled false
```

Now let's start iPerf in Server mode.
```powershell
# Start Server | Listening on 5201
/usr/lib/vmware/vsan/bin/iperf3.copy -s -B [IPERF-SERVER-IP]
```

Now go to the other ESXi Host and run the client.
```powershell
# Start Client
/usr/lib/vmware/vsan/bin/iperf3 -t 10 -c [IPERF-SERVER-IP]
```

You should see a summary of the Interval, Data Transferred and Bandwidth of the sender and receiver.

![]({{site.baseurl}}/img/bandwidthsummary.png)