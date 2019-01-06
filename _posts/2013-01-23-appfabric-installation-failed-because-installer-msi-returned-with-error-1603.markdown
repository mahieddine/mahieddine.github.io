---
layout: post
title:  "AppFabric installation failed because installer MSI returned with error code : 1603 [Windows AppFabric]"
date:   2013-01-23 20:00:23 +0700
categories: [dotnet]
---

When i was about to install Windows AppFabric 1.1 i've gotten this error message : 
```PowerShell
AppFabric installation failed because installer MSI returned with error code : 1603 
```
This error gave me headache, it turns out that this happens because the environment variable “PSModulePath” is not filled correctly (don’t ask me why) so to resolve this issue all you have to do is change the Environment variable 
```PowerShell
“PSModulePath” 
```
value to  
```PowerShell
%SYSTEMROOT%\System32\WindowsPowerShell\v1.0\
```
