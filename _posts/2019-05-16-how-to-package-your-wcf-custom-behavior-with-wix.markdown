---
layout: post
title:  "How to package your WCF-Custom Behavior with WIX"
date:   2019-05-16 23:41:00 +0700
categories: [biztalk,eai,experiments]
comments: true
---


Developping a WCF-Custom behavior without packaging it into a beautiful autosufficient msi is like cooking without cleaning the kitchen behind you, it's bad and dirty :) 

So be nice to your mate and take 30 minutes to package your stuff. 
Deploying a WCF-Custom behavior requires deploying an assembly which is easy to do and editing the machine.config file to include the newly created behavior which is the cumbersome task that we have to deal with, fortunatly there is [WIX toolset (Windows Installer XML)](https://wixtoolset.org/) which will helps a lot to deal with that.

So let's get started, first you have to create a new WIX Setup Library Project  

![](/static/img/upload/how-to-package-your-wcf-custom-behavior-with-wix/create-new-wix-project?:xl:left:)  

Give it a nice name and hit ok, now a new project is going to be created, this project contains only one xml file named Product.wxs and this is all we need to generate our msi

Next just edit it like below based on your needs

```xml 
<?xml version="1.0" encoding="UTF-8"?>
<Wix xmlns="http://schemas.microsoft.com/wix/2006/wi" xmlns:util="http://schemas.microsoft.com/wix/UtilExtension" >
  <Product Id="*" Name="[PUT HERE YOUR PROJECT NAME]" Language="1033" Version="1.0.0.0" Manufacturer="[YOU CAN PUT HERE YOUR NAME OR ORGANISATION]" UpgradeCode="5e155126-c2a4-4da0-b6da-e9626363f32e">
    <Package InstallerVersion="200" Compressed="yes" InstallScope="perMachine" />

    <MajorUpgrade DowngradeErrorMessage="A newer version of [ProductName] is already installed." />
    <MediaTemplate EmbedCab="yes" />

    <Feature Id="ProductFeature" Title="[PUT HERE YOUR PROJECT NAME]" Level="1">
      <ComponentGroupRef Id="ProductComponents" />
    </Feature>
  </Product>

  <Fragment>
    <Directory Id="TARGETDIR" Name="SourceDir">
      <Directory Id="ProgramFilesFolder">
        <Directory Id="INSTALLFOLDER" Name="[PUT HERE YOUR WANT FOR THE INSTALL FOLDER]" />
      </Directory>
    </Directory>
  </Fragment>

  <Fragment>
    <ComponentGroup Id="ProductComponents" Directory="INSTALLFOLDER">
      <Component>
        <File Source="[PUT HERE THE RELATIVE PATH FOR THE ASSEMBLY]" Assembly=".net" KeyPath="yes" />
      </Component>

      <Component Id="MachineConfig4x64" Guid="F39985C8-9D3A-41F3-9330-E30274D4AD23" KeyPath="no" >
        <File Id="MachineConfig4x64.config" Name="MachineConfig4x64.config" Vital="yes" KeyPath="yes" Source="C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config\machine.config" />
        <util:XmlConfig  Id="Machine_Config4x64_Xml_Root"
          File="[WindowsFolder]Microsoft.NET\Framework64\v4.0.30319\CONFIG\Machine.Config"
          Action="create"
          On="install"
          ElementPath="//configuration/system.serviceModel/extensions/behaviorExtensions"
          Name="add"
          Node="element"
          Sequence="1">
        </util:XmlConfig>
        
        <util:XmlConfig Id="Machine_Config4x64_Xml_2"
        File="[WindowsFolder]Microsoft.NET\Framework64\v4.0.30319\CONFIG\Machine.Config"
        ElementPath="Machine_Config4x64_Xml_Root"
        Name="name"
        Value="[PUT HERE THE NAME OF YOUR WCF CUSTOM BEHAVIOR]"
        Sequence="2">
        </util:XmlConfig>
        <util:XmlConfig Id="Machine_Config4x64_Xml_3"
        File="[WindowsFolder]Microsoft.NET\Framework64\v4.0.30319\CONFIG\Machine.Config"
        ElementPath="Machine_Config4x64_Xml_Root"
        Name="type"
        Value="[PUT HERE THE FQN OF YOUR ASSEMBLY e.g MyGreatOrganisation.MyCustomBehaviorExtension.MyExtension, MyGreatOrganisation.MyCustomBehaviorExtension, Version=1.0.0.0, Culture=neutral, PublicKeyToken=d53594425439f67a]"
        Sequence="3">
        </util:XmlConfig>
        <util:XmlConfig Id="Machine_Config4x64_Xml_Uninstall_1"
        File="[WindowsFolder]Microsoft.NET\Framework64\v4.0.30319\CONFIG\Machine.Config"
        Action="delete"
        On="uninstall"
        ElementPath="//configuration/system.serviceModel/extensions/behaviorExtensions"
        Node="element"
        VerifyPath="add[\[]@name='[PUT HERE YOUR WCF CUSTOM BEHAVIOR]'[\]]"
        Sequence="1">
        </util:XmlConfig>
      </Component>
      <Component Id="MachineConfig4x86" Guid="74E40DBF-DEB3-4E71-91D5-DBB7B1451CC2" KeyPath="no" >
        <File Id="MachineConfig4x86.config" Name="MachineConfig4x86.config" Vital="yes" KeyPath="yes" Source="C:\Windows\Microsoft.NET\Framework\v4.0.30319\Config\machine.config" />
        <util:XmlConfig  Id="Machine_Config4x86_Xml_Root"
          File="[WindowsFolder]Microsoft.NET\Framework\v4.0.30319\CONFIG\Machine.Config"
          Action="create"
          On="install"
          ElementPath="//configuration/system.serviceModel/extensions/behaviorExtensions"
          Name="add"
          Node="element"
          Sequence="1">
        </util:XmlConfig>
        <util:XmlConfig Id="Machine_Config4x86_Xml_2"
        File="[WindowsFolder]Microsoft.NET\Framework\v4.0.30319\CONFIG\Machine.Config"
        ElementPath="Machine_Config4x86_Xml_Root"
        Name="name"
        Value="[PUT HERE THE NAME OF YOUR WCF CUSTOM BEHAVIOR]"
        Sequence="2">
        </util:XmlConfig>
        <util:XmlConfig Id="Machine_Config4x86_Xml_3"
        File="[WindowsFolder]Microsoft.NET\Framework\v4.0.30319\CONFIG\Machine.Config"
        ElementPath="Machine_Config4x86_Xml_Root"
        Name="type"
        Value="[PUT HERE THE FQN OF YOUR ASSEMBLY e.g MyGreatOrganisation.MyCustomBehaviorExtension.MyExtension, MyGreatOrganisation.MyCustomBehaviorExtension, Version=1.0.0.0, Culture=neutral, PublicKeyToken=d53594425439f67a]"
        Sequence="3">
        </util:XmlConfig>
        <util:XmlConfig Id="Machine_Config4x86_Xml_Uninstall_1"
        File="[WindowsFolder]Microsoft.NET\Framework\v4.0.30319\CONFIG\Machine.Config"
        Action="delete"
        On="uninstall"
        ElementPath="//configuration/system.serviceModel/extensions/behaviorExtensions"
        Node="element"
        VerifyPath="add[\[]@name='[PUT HERE THE NAME OF YOUR WCF CUSTOM BEHAVIOR]'[\]]"
        Sequence="1">
        </util:XmlConfig>
      </Component>
      <Component Id="MachineConfig2x64" Guid="A39985C8-9D3A-41F3-9330-E30274D4AD23" KeyPath="no" >
        <File Id="MachineConfig2x64.config" Name="MachineConfig2x64.config" Vital="yes" KeyPath="yes" Source="C:\Windows\Microsoft.NET\Framework64\v2.0.50727\Config\machine.config" />
        <util:XmlConfig  Id="Machine_Config2x64_Xml_Root"
          File="[WindowsFolder]Microsoft.NET\Framework64\v2.0.50727\Config\machine.config"
          Action="create"
          On="install"
          ElementPath="//configuration/system.serviceModel/extensions/behaviorExtensions"
          Name="add"
          Node="element"
          Sequence="1">
        </util:XmlConfig>

        <util:XmlConfig Id="Machine_Config2x64_Xml_2"
        File="[WindowsFolder]Microsoft.NET\Framework64\v2.0.50727\Config\machine.config"
        ElementPath="Machine_Config2x64_Xml_Root"
        Name="name"
        Value="[PUT HERE THE NAME OF YOUR WCF CUSTOM BEHAVIOR]"
        Sequence="2">
        </util:XmlConfig>
        <util:XmlConfig Id="Machine_Config2x64_Xml_3"
        File="[WindowsFolder]Microsoft.NET\Framework64\v2.0.50727\Config\machine.config"
        ElementPath="Machine_Config2x64_Xml_Root"
        Name="type"
        Value="[PUT HERE THE FQN OF YOUR ASSEMBLY e.g MyGreatOrganisation.MyCustomBehaviorExtension.MyExtension, MyGreatOrganisation.MyCustomBehaviorExtension, Version=1.0.0.0, Culture=neutral, PublicKeyToken=d53594425439f67a]"
        Sequence="3">
        </util:XmlConfig>
        <util:XmlConfig Id="Machine_Config2x64_Xml_Uninstall_1"
        File="[WindowsFolder]Microsoft.NET\Framework64\v2.0.50727\Config\machine.config"
        Action="delete"
        On="uninstall"
        ElementPath="//configuration/system.serviceModel/extensions/behaviorExtensions"
        Node="element"
        VerifyPath="add[\[]@name='[PUT HERE THE NAME OF YOUR WCF CUSTOM BEHAVIOR]'[\]]"
        Sequence="1">
        </util:XmlConfig>
      </Component>
      <Component Id="MachineConfig2x86" Guid="84E40DBF-DEB3-4E71-91D5-DBB7B1451CC2" KeyPath="no" >
        <File Id="MachineConfig2x86.config" Name="MachineConfig2x86.config" Vital="yes" KeyPath="yes" Source="C:\Windows\Microsoft.NET\Framework\v2.0.50727\Config\machine.config" />
        <util:XmlConfig  Id="Machine_Config2x86_Xml_Root"
          File="[WindowsFolder]Microsoft.NET\Framework\v2.0.50727\Config\machine.config"
          Action="create"
          On="install"
          ElementPath="//configuration/system.serviceModel/extensions/behaviorExtensions"
          Name="add"
          Node="element"
          Sequence="1">
        </util:XmlConfig>
        <util:XmlConfig Id="Machine_Config2x86_Xml_2"
        File="[WindowsFolder]Microsoft.NET\Framework\v2.0.50727\Config\machine.config"
        ElementPath="Machine_Config2x86_Xml_Root"
        Name="name"
        Value="[PUT HERE THE NAME OF YOUR WCF CUSTOM BEHAVIOR]"
        Sequence="2">
        </util:XmlConfig>
        <util:XmlConfig Id="Machine_Config2x86_Xml_3"
        File="[WindowsFolder]Microsoft.NET\Framework\v4.0.30319\CONFIG\Machine.Config"
        ElementPath="Machine_Config2x86_Xml_Root"
        Name="type"
        Value="[PUT HERE THE FQN OF YOUR ASSEMBLY e.g MyGreatOrganisation.MyCustomBehaviorExtension.MyExtension, MyGreatOrganisation.MyCustomBehaviorExtension, Version=1.0.0.0, Culture=neutral, PublicKeyToken=d53594425439f67a]"
        Sequence="3">
        </util:XmlConfig>
        <util:XmlConfig Id="Machine_Config2x86_Xml_Uninstall_1"
        File="[WindowsFolder]Microsoft.NET\Framework\v2.0.50727\Config\machine.config"
        Action="delete"
        On="uninstall"
        ElementPath="//configuration/system.serviceModel/extensions/behaviorExtensions"
        Node="element"
        VerifyPath="add[\[]@name='[PUT HERE THE NAME OF YOUR WCF CUSTOM BEHAVIOR]'[\]]"
        Sequence="1">
        </util:XmlConfig>
      </Component>
    </ComponentGroup>
  </Fragment>
</Wix>
```

Compile your project and that's it, this will generate a nice msi, that once executed will GAC your assembly and add a reference to your newly created behavior in the different machine.config files present on your machine. 

What's interessting is that installing your msi means that the system will also keep a reference to your package and that means when you will uninstall it, your behavior will be removed from all the machine.config files which keeps everything clean from unused stuff 

That's it 
