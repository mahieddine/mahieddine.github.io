---
layout: post
title:  "Implementing an integration Solution with Workflow Manager/Service Bus and BizTalk 2010R2/2013 – Part 1"
date:   2013-03-11 20:00:23 +0700
categories: [eai]
---

### Introduction:

Recently Microsoft Introduced Workflow Manager and the new version of Service Bus, for those who don’t already know what Service Bus is ? Service Bus offers a reliable, secured and highly available hosted communication infrastructure, it also offer a sort of big event infrastructure hub. Based on the pub/sub pattern Service Bus offers many tools for your application’s communication scenarios like Queues, Topic, and Event. Service Bus keeps messages in safe until they are consumed, so theoretically you will never lose a single message 🙂

Workflow Manager can host Workflows in a hosted Environment; Workflows must be created in .net 4.5. because Workflow Manager doesn’t support VB Expression which has been replaced by C# Expression in .net 4.5

You must know that Workflow Manager uses a notification mechanism (We will see it later) to activate/continue a workflow instance so it relies on Service Bus to do this.

Workflow Manager and Service Bus comes in two version one available in Azure Cloud and an On-Premise version.

BizTalk Server is a well-known product I think I don’t need to present it; BizTalk Server 2013 comes with a set of adapter out of the box to consume messages from Service Bus. If you tried before to integrate BizTalk Server with Service Bus you probably know the “SB-messaging” adapter, the main problem with this adapter is that Microsoft Presents it as a adapter that can be used for both Service Bus in Azure and On-Premise version, in reality you can only use it with Azure version.

Paolo Salvatori has made a remarkable workaround to connect BizTalk Server with Service Bus by Developping binding Extension to overcome this issue, he also implemented a Short Integration Scenario for this purpose that you can find here http://code.msdn.microsoft.com/windowsdesktop/How-to-integrate-BizTalk-07fada58#content but I wanted to go further by putting the focus on Service Bus / Workflow Manager/BizTalk Server 2013 and showing you their limitations and how I encountered them, I will implement a real workflow hosted in Workflow Manager 1.0, I Will show you how you can debug a Workflow in Workflow Manager 😉 and how it works ?  I’ll Develop a little BizTalk Application and connect it with my workflow using Service Bus For Windows Server. This is a big article and I’m going to divide it into 2 parties first the installation and setup environment and the second one for implementing the scenario, so take your breath. Take a big cup of coffee and let’s go 🙂

### First To implement our scenario we need  

#### 1 – Prerequisite
+ Windows Server 2012 / 2008 R2 / SQL Server 2012
+ Service Bus for windows Server (1.8)
+ You can download it [here](http://www.microsoft.com/fr-fr/download/details.aspx?id=35374)
+ Workflow Manager 1.0, you can find it [here](http://www.microsoft.com/fr-fr/download/details.aspx?id=35375)

Workflow Client 1.0 contains the core assemblies and client API for Workflow 1.0
Workflow Manager Tools contains a set of tool to debug your workflow in Workflow Manager; we will see later how you can use it.

*Windows AppFabric 1.1

You can find it [here](http://www.microsoft.com/fr-fr/download/details.aspx?id=27115)

Now we can install and configure Workflow Manager and Service Bus,  you must know that configuring workflow manager will configure automatically service bus.

so you have to go and launch “Workflow Manager Configuration” and choose “Configure Workflow Manager with Default Settings”, then it’s just classic next next 🙂

![](/static/img/upload/implementing-an-integration-solution-with-workflow-manager-part1/install-workflow-step1.jpg)
TODO !!
If you encounter an error during the installation take a look here http://192.168.1.16/2013/01/23/appfabric-installation-failed-because-installer-msi-returned-with-error-code-1603-windows-appfabric/

*BizTalk Server 2013 Beta

Here is the link http://www.microsoft.com/en-us/download/details.aspx?id=35553

#### 2 – Post Installation Checklist: 
After finishing the installation you have to verify this check list items

**Service Bus:**
Open Service Bus PowerShell Prompt and type the [following command](http://msdn.microsoft.com/en-us/library/windowsazure/jj248748(v=azure.10).aspx):

```PowerShell
Get-SBFarmStatus
```
If you correctly installed it you should see Service Bus Services up and running
```PowerShell
HostId HostName                ServiceName              Status
—— ——–                         ———–                       ——
1 WIN-IC2B10UV7UB…. Service Bus Gateway                 Running
1 WIN-IC2B10UV7UB…. Service Bus Mess…                   Running
1 WIN-IC2B10UV7UB…. FabricHostSvc                       Running
```

If you don’t you should start these two service bus services:

![](/static/img/upload/implementing-an-integration-solution-with-workflow-manager-part1/service-bus-services.png)

**Workflow Manager:**
Open Service Bus PowerShell Prompt and type the [following command](http://msdn.microsoft.com/en-us/library/windowsazure/jj248748(v=azure.10).aspx):  

```PowerShell
Get-WFFarmStatus
``` 
If your installation is ok you should see this  

```Shell
HostId HostName                ServiceName              Status
—— ——–                         ———–                        ——
1 WIN-IC2B10UV7UB…. WorkflowServiceBackend              Running
1 WIN-IC2B10UV7UB…. WorkflowServiceFrontEnd..           Running
```
If not you should probably start the Workflow Manager Back End Service

Now you need to get this BindingExtensions or get the source [here](http://code.msdn.microsoft.com/windowsdesktop/How-to-integrate-BizTalk-07fada58) and compile them.

Then you need to GAC them

Open Visual Studio Command Prompt and type:  

```PowerShell
gacutil /i dll_name
```
The final Step is to register these bindings extensions in your machine.config (32/64bits, .net framework 4.0), to make it easy for you, you can find [here](/static/files/upload/machine.zip) my machine.config file

That’s it if you correctly setup your environment now, in the next part we are going to implement our solution.
