---
layout: post
title:  "Build a Biztalk solution based on WCF-SQL notification"
date:   2012-07-11 20:18:23 +0700
categories: [eai]
comments: true
---
When you design a biztalk solution and need to launch process based on changes that occures in database you have not so much choice and you are certainly going to choose between two solutions :

## 1- Polling based solution :
If your polling request is fast enought and if you know that every 30 secondes for example your are sure to get something to process and not surcharging processor for nothing  then its a good solution to discover database changes but it’s not always the case.

## 2 – SQL Notification based solution :
thanks to WCF-SQL Adapter and SQL Broker you can detect database changes and do whatever you want further, in this article we are going to see everything you need to build a complete Biztalk Solution Based on WCF-SQL notification and the current serious problem and troubles that you may get in when you use this

First I assume you have WCF-SQL Adapter already installed on your Biztalk Server  if it’s not the case i invite you to dowload it and install it from [here](http://social.technet.microsoft.com/wiki/contents/articles/6781.biztalk-adapter-pack-2010-wcf-sql-adapter-en-us.aspx)

After installing WCF-SQL Adapter you must configure your port
![WCF Notification Port Configuration](/static/img/upload/wcf-notification/port-configuration.png)

So in Inboud you set it to “Notification” and in Notification Statement you define your SQL Query on which you activate a notification, here are some precisous informations that can save you many time :

– Your SQL Notification Query must be conform to this [http://msdn.microsoft.com/en-us/library/ms181122(SQL.105).aspx](http://msdn.microsoft.com/en-us/library/ms181122(SQL.105).aspx)

– If the request returns always the same things like where 1=1 or something like this, this is not going to work!

– If your SQL request contains a join between one or many tables on different criteria lets say for instance select a,b from tablea inner join tablea.fielda = tableb.fieldb you are not going to have a notification until fielda and fieldb change both and are equal if just one of them changes and even if fielda=fieldb **you will not get any notification** this is something to consider and little be anoying.

So now when you activate your receive location the WCF SQL adapter will create a service Queue with a guid and manage all the traditionnal aspects to deal with the SQL Broker

Next we are going to activate the **SQL Broker** the problem with this is activating it requires that no one uses the database this is impossible especially when you are in Developpement Environnement so what we do is force the database to go in single user mode activate it and then go in multiuser mode again.

Remark : when you activate your WCF-SQL notification port this create a Service Queue with a Guid, disabling Service Broker doesn’t delete it until the next Start of the service broker and this may cause you some trouble when you have an automatic build so what we do first is a Prescript that disable enable and disable again service broker before the build and the activate it after the build completes.

```SQL
ALTER DATABASE STAGING_BTS SET SINGLE_USER WITH ROLLBACK IMMEDIATE
ALTER DATABASE STAGING_BTS SET DISABLE_BROKER
ALTER DATABASE STAGING_BTS SET MULTI_USER 
/****************************************/
ALTER DATABASE STAGING_BTS SET SINGLE_USER WITH ROLLBACK IMMEDIATE
ALTER DATABASE STAGING_BTS SET ENABLE_BROKER
ALTER DATABASE STAGING_BTS SET MULTI_USER
/********************************/
ALTER DATABASE STAGING_BTS SET SINGLE_USER WITH ROLLBACK IMMEDIATE
ALTER DATABASE STAGING_BTS SET DISABLE_BROKER
ALTER DATABASE STAGING_BTS SET MULTI_USER
```
the problem with this approche is that you disconnect all users automatically each time a build occures so what we do is delete thos scripts and just enable the “Service Broker” in the database project and this works

Now everytime a changes in database occurres you will receive a notifcation message like this
![promote](/static/img/upload/wcf-notification/map-promotion.png)

**Info :**  contains the sql action that has been done on the table you are watching. Can be Insert, Update and more (http://msdn.microsoft.com/en-us/library/system.data.sqlclient.sqlnotificationinfo.aspx)  
**Source :** contains the if it is data, object or something else that is the course for the notification: http://msdn.microsoft.com/en-us/library/system.data.sqlclient.sqlnotificationsource.aspx  
**Type :**  contains the type of notification mostly change http://msdn.microsoft.com/en-us/library/z0fkxc6y.aspx
You should promote at least info and source element, so that you can use these fields for routing.  

Next all you need is to define a stored procedure that poll data to process every time you have a notification

**Remark :**  SQL Server doesn’t manage cluster features so if you have two nodes you will have two notifications and then two call for your stored procedure so your stored procedure must manage this to process data only once !

⚠ Some problems you may be confronted with are :

– When you have serious traffic and many notifications Deadlock on the Service Queue is a monster that you may be confronted with, and this is absolutly an unmanagable issue, the only thing you can do is either use SQL Hint in your SQL Request (UPDLOCK, READLOCK) on the SQL Request related to the tables present in your SQL Notification Query this generally work if this doesn’t work always for you the only thing you can do is to force SQL Server to execute only one instance at a time of your check stored procedure.

– Don’t try to  solve the issue above with puting “with nolock” in your SQL Notification this will simply kill your Biztalk immediatly.
