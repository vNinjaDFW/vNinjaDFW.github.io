---
layout: post
title:  Datacenter Power Consumption - vROPs
date:   2020-03-23-dcpowerusage
image:  
tags:   [vExpert, vROPs]
---
Today, I was asked by my client for a way to produce a power consumption report on their ESXi Hosts by Cluster. I wasn't sure initially if this was even possible, but after a quick search, I found a great launch point on the [vRealize Operations Sample Exchange](https://vrealize.vmware.com/sample-exchange/). I'm not going to reinvent the wheel here, but I'm going to list out the steps I took and what my Dashboard looked like when it was completed.

<h5>Enable the Metrics in the Policy (Watt)</h5>

1. Login to vROPs  
   _Verify that you1 have the necessary access rights to perform this task. Your vRealize Operations Manager administrator can tell you which actions you can perform._
2. After login, click on Administration  

![]({{site.baseurl}}/img/vrops_1.png)

3. Goto Policies & Policy Library  

![]({{site.baseurl}}/img/vrops_2.png)

4. Click on the Policy assigned to your Hosts (usually Default)
5. Click on Edit & goto "Collect Metrics and Properties"  
   _You might need to expand your screen here to make sure you can see the "Filter" option_
6. Type "Watt" in the Filter and hit <ENTER>
7. Make sure the "State" column shows "Local" and hit <ENTER>  

![]({{site.baseurl}}/img/vrops_3.png)

<h5>Import the View into vROPs</h5>

1. Click Dashboards at the top & Views on the left sidebar  

![]({{site.baseurl}}/img/vrops_4.png)

2. Click the gear icon and select Import View  

![]({{site.baseurl}}/img/vrops_5.png)

3. Browse to select the downloaded XML file and click Import  
   _The imported view overwrites if a view with the same name exists. All report templates that use the existing view are updated with the imported view._  
       
![]({{site.baseurl}}/img/vrops_5a.png)

<h5>Import the Dashboard into vROPs</h5>

1. Click Dashboards, Actions dropdown, and select Manage Dashboards  

![]({{site.baseurl}}/img/vrops_6.png)

2. Click on the gear icon and select Import Dashboards  

![]({{site.baseurl}}/img/vrops_7.png)

3. Browse to select the downloaded json file for the dashboard you want to import  

![]({{site.baseurl}}/img/vrops_7a.png)

After data has refreshed into the collection, your Dashboard should similar to this:  

![]({{site.baseurl}}/img/vrops_dash.png)
