---
layout: post
title:  "Implementing an integration Solution with Workflow Manager/Service Bus and BizTalk 2010/2013 – Part 2"
date:   2013-05-18 20:00:23 +0700
categories: [eai]
---

### Workflow Manager 

In this article we are going to view :

1. Prerequisite
2. What is workflow manager ? 
3. How does it work ? 
4. Implement a simple “OrderProcess” Workflow 
5. How can i host my Workflow in Workflow Manager ?
6. How can i debut my Workflow in Workflow Manager ?


### 1 – Prerequisite :
If you didn't already installed Workflow Manager I invite you to install it and set up your environment, you can found all the necessary information to do it  on [/eai/2013/03/11/implementing-an-integration-solution-with-workflow-manager-service-bus-and-biztalk-2010R2-2013-part-1.html](/eai/2013/03/11/implementing-an-integration-solution-with-workflow-manager-service-bus-and-biztalk-2010R2-2013-part-1.html)

### 2 -What is workflow manager ? 
Currently if you want to host a .net workflow you have tree different solutions : Workflow Application, Workflow Service Host and the new Workflow manager each one is designed for a specific purpose, if you take Workflow Application for example is used for async execution of a single workflow, Workflow Service Host is used for Async execution of multiple workflow instance of a single definition.

Workflow Manager is for multi-tenant, scalability hosting of workflows, it supports high scale and high density execution. Workflow Manager is built on the Windows Workflow Foundation programming model, runtime and activity library in the .NET Framework.

Workflow Manager hosts only workflow written in .net 4.5 !

### 3 -How does it work ? 
Workflow Manager is composed of tree main components that guarantee the scalability :

SQL Server, WF BackEnd, ServiceBus and all theses components exposed via WF Gateway on IIS which enable you basically the define the entrance point, manager workflows, activities…Etc. Of course each component can scale differently.

Workflow Manager relies on ServiceBus and the Pub/Sub Pattern to  Create/Continue a Workflow Instance. Workflow Manager uses notification mechanism to achieve this, we will see later on in this article.

### 4 -Implement a simple OrderProcess Workflow :
We are going now to implement a very simple solution to see how it works :

Create a new solution:

File -> New -> Project -> Workflow Console Application

Create a new Argument in your workflow, name it : OrderId (Int32)

Put a Sequence Chart, put an Assign statement and Create a new Variable, name it OrderToProcess (Int32) in the Assign statement, assign OrderId to OrderToProcess

Now we are going to define a Custom Activity to publish our notification,

to achieve this i’ve created a short library that perform the basic tasks such as : connect to WF Manager, publish a workflow, publish a notification.

now to fire our workflow we have to publish it in workflow manager and specify the subscription key.

### 6 -How can i debut my Workflow in Workflow Manager ?
You can’t debug your workflow that is hosted on workflow manager, to debug your workflow you have to download : WF\WorkflowClient.exe et WF\WorkflowManagerTools.exe available here [http://www.microsoft.com/fr-fr/download/details.aspx?id=35375](http://www.microsoft.com/fr-fr/download/details.aspx?id=35375)

Then you have to install them.

Next step is launch via cmd Workflow Manager Tools.exe this will emulate workflow manager by creating fake database/tables necessary for running workflow manager

Then all you have to do is publish your workflow in Workflow Manager tools rather than publishing it in Workflow Manager, then you can attach your visual studio with the “console of workflow manager tools” and debug easily your workflow

Once i finish my library documentation i will publish it sooner…Stay tuned

In the last part we will see how to implement our solution on BizTalk Server 2013, i hope i’ll have enough time to publish it

 
