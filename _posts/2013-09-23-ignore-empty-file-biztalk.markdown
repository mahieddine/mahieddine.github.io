---
layout: post
title:  "Ignoring an empty file in BizTalk"
date:   2013-09-23 20:00:23 +0700
categories: [eai]
comments: true
---
Hi,

One of the main need in BizTalk’s Application Development is the ability to receive an empty file without any error and sometimes also the ability to simply ignore it. Unfortunately BizTalk doesn’t offer this type of feature natively,  so i’ll try to share with you how i do it and also how you can put this in practice in your daily BizTalk application development.

This method has been tested on both FILE and FTP Adapter (both Microsoft and nSoftware)

So here is the big picture :

Custom Receive Pipeline  ===> Process Send Port (Message not empty)
                         ===> Trash Send Port (Message Empty)

First we are going to put our “ProcessEmptyMessage” Custom pipeline  in the decode stage that custom pipeline basically will assign a default message  to the entry message only if the latter is empty and will also add a context property to be able to route the message to   either the “trash send port” or the “process send port”

**Requirements :**

Download  these two pipeline components :

+ [https://github.com/mahieddine/empty-message-processor](https://github.com/mahieddine/empty-message-processor)
+ [https://eebiztalkpipelinecom.codeplex.com/](https://eebiztalkpipelinecom.codeplex.com)

So first we add a the “ProcessEmptyMessage” custom pipeline component in the decode stage, this custom pipeline takes 3 optional parameters  :

**DefaultMessage :** this message is assigned to the message if and only if the entry message is empty.

**ContextPropertyName, ContextPropertyNameSpace :** you can put here a property that you want to promote, this property will take a boolean value that indicates if the entry message is empty or not.  This property will serve us to route the empty message to the “trash send port”

On the other side you create a TrashSendPort, then add send pipeline then drag&drop the dev null custom custom pipeline component in the encode stage.

Set the TrashSendPortFilter to Ournamespace.IsEmpty = true and the ProcessSendPort’s Filter to Ournamespace.IsEmpty = false

Now every empty message will be automatically dropped, if you have many applications that need to drop a message you can create a shared biztalk application that plays the “Trash” Role

Thank you !
