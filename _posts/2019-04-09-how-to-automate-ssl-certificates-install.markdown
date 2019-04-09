---
layout: post
title:  "How to automate SSL Certificates install"
date:   2019-04-09 23:41:00 +0700
categories: [biztalk,eai,experiments]
comments: true
---

Sometimes you might need to automate the SSL certificates installation, on windows you can achieve that in a simple manner with the [CERTUTIL](https://docs.microsoft.com/en-us/windows-server/administration/windows-commands/certutil) command utility

Here is a snippet of how i personally do it in a simple bat file

```bat
@echo off  
REM here i define the list of certificates to install  
SET CERT_LIST=".\Cert1Path.cer" ".\Cert2Path.cer" ".\Cert3Path.crt"   
```

next if you want to import them to the **Trusted Root Certification Authorities** on Local Machine

```bat
REM Import a certificate to the “Trusted Root Certification Authorities” on Local Machine
(for %%certPath in (%CERT_LIST%) do ( 
  CERTUTIL -addstore -enterprise -f -v root %%certPath
))
```

or If you want to import them to the **Trusted People** on Local Machine   

```bat
REM Import a certificate to the Trusted People on Local Machine
(for %%certPath in (%CERT_LIST%) do ( 
  CERTUTIL -addstore -f “TRUSTEDPEOPLE” -v root %%certPath
))
```

This bat of course can be embedded as a post install task in a msi or whatever you want based on your deployment methodology.

It's that simple 




