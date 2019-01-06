---
layout: post
title:  "Custom BizTalk XML Declaration"
date:   2013-09-23 20:00:23 +0700
categories: [eai]
comments: true
---

Here is a nice little trick,  imagine you produce an xml file like this :

```XML
<?xml version="1.0"?>
<books>
<book author="toto" title="titi" />
</book>
```
Now imagine you if have to set the output xml declaration to

```XML
<?xml version=”1.0″ standalone=”no” ?>
```

Many of us will directly develop a custom pipeline to do this while you can simply do it with setting some properties in the XML Assembler.

YES you heard that, you can do it by setting just two magic properties :

First we say to the XML Assembler hey don’t add the XML Declaration, then set in the Add processing instructions text property all what you want to add in the XML Declaration.

**Remark :** All those instructions must start with a “<?” and end with a “?>”  
![](/static/img/upload/custom-biztalk-xml-declaration/settings.png)

That’s it
