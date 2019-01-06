---
layout: post
title:  "Biztalk CTP for BizTalk 2012 is out !"
date:   2012-07-18 19:18:23 +0700
categories: [eai]
---
Hi,
BizTalk CTP for BizTalk 2012 is out ! and is available for Microsoft internally and some special members only, the CTP should be available for public around October 2012 and RTM certainly in January -February 2013, in the meantime you can check the novelties for the future BizTalk’s version, i copy/past the release email from Microsoft (don’t ask me how did i get it ) 😀  
  

> ### Improved productivity with new Microsoft Platform support
> 
> Customers can now leverage the latest and greatest platforms, such as Windows Server 2012 RC, SQL Server 2012, Visual Studio 2012 RC. All new BizTalk projects will target .Net Framework 4.5 RC by default. The CTP also provides support for latest LOB versions enabling customers to use BizTalk for integrating their applications with the latest versions of SAP, Oracle and SQL Server. The new adapters provide a seamless experience to enable hybrid connectivity, all done via configuration. The CTP provides native support for ACS authentication and is extensible for other authentication mechanisms.
> 
> ### Platform support
> 
> o Windows Server 2012 RC, Windows Server 2008 R2
> o SQL Server 2012, SQL Server 2008 R2
> o Visual Studio 2012 RC
> o Office 2010
> o Support for latest LOB versions
> o Support for SQL Server 2012
> o Support for SAP 7.2
> o Support for Oracle DB 11.2
> o Support for Oracle EBS 12.1 …
> 
> ### Adapters
> 
> o WCF-WebHttp adapter, to consume REST service or expose REST service
> 
> o SB-Messaging, for sending/pulling data from Service Bus Queues/Topics
> 
> o WCF-NetTCPRelay, for hosting relays or sending data to NetTCPRelay end points
> 
> o WCF-BasicHttpRelay, for hosting relays or sending data to BasicHttpRelay end points
> 
> ### Better B2B with schema updates
> 
> EDI standards evolve and one of the key investments made in this new BizTalk CTP is to ensure that we support the latest B2B standards natively. This enables you to transact messages based on the latest versions of EDI protocol.
> 
> o B2B enhancements to support latest standards natively
> 
> o Support for X12 5040, 5050, 6020, 6030
> 
> o Support for EDIFACT D06A, D06B, D07A, D07B, D08A, D08B, D09A, D09B, D10A, D10B
> 
> o HL7 2.5.1
> 
> We are working on further schema updates such as HL7 2.6, these will be enabled in the BizTalk 2010 R2 Beta.
> Improved Performance
> 
> The CTP provides performance improvement for certain key scenarios. In case of two way MLLP adapter scenarios where ordered delivery is set, the tests have revealed up-to 5X performance improvement so far in our environments. We have also made enhancements in our engine to improve the performance in ordered send port scenarios.
> 
> ### Building hybrid applications
> 
> Today, there is an increase in the adoption of hybrid application scenarios where some components of an application run in the cloud and some other components/LOB applications remain on-premise. It then becomes important to integrate between these components and leverage the richness of both worlds. In this CTP release, we enable hybrid connectivity by providing first class support for integrating with Azure Service Bus Queues/Topics/Relays. We are introducing the following adapters
> 
> · SB-Messaging, for sending/pulling data from Service Bus Queues/Topics
> 
> · WCF-NetTCPRelay, for hosting relays or sending data to NetTCPRelay end points
> 
> · WCF-BasicHttpRelay, for hosting relays or sending data to BasicHttpRelay end points
> 
> Integrating with Azure Service Bus entities is now just a few configurations away!
> 
> ### Integration with RESTful services
> 
> One of the other prevalent trends in the market today is the proliferation of RESTful services. Almost all new services, as well a lot of services created previously, have a REST interface exposed. For example, all services in Windows Azure, data market place, Salesforce, etc. have support for REST services. With this CTP release, we are making it really easy for you to integrate RESTful services with BizTalk Server using the new WCF-WebHttp adapter. All the REST operations like GET, PUT, POST and DELETE are now supported natively. It gets better. We received community feedback during and post TechEd conference that there should be a way to expose REST services as well from BizTalk. We listened to your feedback. Along with consuming REST servicesm we are also really excited to announce that you now have an early preview to exposing REST services from BizTalk Server as well in this CTP.
> BizTalk Server in Azure Virtual Machine role
> 
> All the above enhancements are available right away for you to preview with BizTalk Server in Azure Virtual Machine role. Setting up a new BizTalk Server environment usually involves long lead time to procure hardware, get the dependencies in place, set up the server, etc. This means long lead times before you can get started with your new BizTalk Server environment. We are now leveraging the power of the cloud and the richness of Windows Azure to provide an experience where you can get up and running with your BizTalk Server environment in matter of minutes and move your existing applications to the cloud without making any changes. Furthermore, the CTP provide improvements to the BizTalk multi machine configuration and now you can do this using some basic configuration settings with the click of a button in a single machine, without having to go and configure BizTalk Server Group in each of the individual nodes.

Stay tuned 
