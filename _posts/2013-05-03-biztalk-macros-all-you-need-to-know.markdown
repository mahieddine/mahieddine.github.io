---
layout: post
title:  "BizTalk Macros – All you need to know"
date:   2013-05-03 20:00:23 +0700
categories: [eai]
---

One of the most powerfull feature of BizTalk is the ability to set dynamic file name thanks to Macro, here you can find the list of all the macros available by default on any BizTalk Server.

| Macro name  | Substitute value | 
| ------------- |-------------|
| %datetime%| Coordinated Universal Time (UTC) date time in the format YYYY-MM-DDThhmmss (for example, 1997-07-12T103508).|
|%datetime_bts2000%|UTC date time in the format YYYYMMDDhhmmsss, where sss means seconds and milliseconds (for example, 199707121035234 means 1997/07/12, 10:35:23 and 400 milliseconds).|
|%datetime.tz%|Local date time plus time zone from GMT in the format YYYY-MM-DDThhmmssTZD, (for example, 1997-07-12T103508+800).|
|%DestinationParty%|Name of the destination party. The value comes from the message context propertyBTS.DestinationParty.|
|%DestinationPartyQualifier%|Qualifier of the destination party. The value comes from the message context propertyBTS.DestinationPartyQualifier.|
|%MessageID%|Globally unique identifier (GUID) of the message in BizTalk Server. The value comes directly from the message context property BTS.MessageID.|
|%SourceFileName%|Name of the file from which the File adapter read the message. The file name includes the extension and excludes the file path, for example, Sample.xml. When substituting this property, the File adapter extracts the file name from the absolute file path stored in the FILE.ReceivedFileName context property. If the context property does not have a value—for example, if a message was received on an adapter other than the File adapter—the macro will not be substituted and will remain in the file name as is (for example, C:\Drop\%SourceFileName%). Correct implementation of this macro requires that the output message is the same message as the received message.|
|%SourceParty%|Name of the source party from which the File adapter received the message. Correct implementation of this macro requires that the output message is the same message as the received message.|
|%SourcePartyQualifier%|Qualifier of the source party from which the File adapter received the message. Correct implementation of this macro requires that the output message is the same message as the received message|
|%time%|UTC time in the format hhmmss.|
|%time.tz%|Local time plus time zone from GMT, In case you want to set your file name based on a context value you can develope a pipeline component to set your own Macro that get this value from the context or whatever and set it to the filename, if i have the time i will publish soon a pipeline component to do this.|

For more details, you can check the official microsoft BizTalk technical guides     
   
+ [http://msdn.microsoft.com/en-us/library/aa578022%28BTS.20%29.aspx](http://msdn.microsoft.com/en-us/library/aa578022%28BTS.20%29.aspx)
+ [http://msdn.microsoft.com/en-us/library/aa578490%28BTS.70%29.aspx](http://msdn.microsoft.com/en-us/library/aa578490%28BTS.70%29.aspx)
