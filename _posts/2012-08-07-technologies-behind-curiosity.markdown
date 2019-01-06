---
layout: post
title:  "Technologies behind Curiosity"
date:   2012-08-07 20:00:23 +0700
categories: [experiments]
---

![](/static/img/upload/technologies-behind-curiosity/robot.jpg)   
Late last night, Mars Science Laboratory (MSL) Curiosity successfully navigated its way through Seven Minutes of Terror and touched down on the surface of the Red Planet, heralding a new age of extraterrestrial exploration.
 A fiew moments later the first images started to come out, and this was the first “public” image
coming from Curiosity.  There is still some dust but it’s normal.

![](/static/img/upload/technologies-behind-curiosity/first_shot.jpg)

Now if you are a geek and curious you may want to know what kind of hardware and software have been involved ? what’s the operating system of this monster ? Which programing language has been used ?

**First the Hardware :** Cursiosity is powered by a RAD750 which is a single-board computer (motherboard, RAM, ROM, and CPU)  manufactured by BAE Systems Electronic Solutions except that it’s highly resistant to a very high level of radiation,  The CPU itself can withstand 2,000 to 10,000 gray and temperature ranges between –55 °C and 125 °C and requires 5 watts of power, This RAD750 has been already used in satellite systems for more than a decade.

The CPU is a PowerPC 750 clocked at around 200MHz,  256MB DRAM and 2GB Flash this looks like a very poor configuration but it’s not, the storage is used as a buffer to first save images and data collected and then stream it to the sattelite and then earth.

**Battery :** Another big challenge is the power supply, robot like this needs a lot of energy and a simple solar pannel is not sufficient especially in short day of winter, a plutonium battery has been developed for more details check out this video.

<iframe width="320" height="180" src="https://www.youtube.com/embed/1JOPW8aAcgE" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

**Operating System :** For this kind of task you need a realtime operating system, NASA tested several RTOS and decided to use VxWorks (6.9) an 27 Years Old OS developed by Wind River System because for it’s very fast interupt response and Runs almost on every modern CPU.

**Software :**  One thing to know NASA are very very very careful about coding, no “clever tricky code” is tolerated unless it’s very very necessary, the code sequences are coded in C and all C code is ISO/IEC 9899-1999 compliant, it’s to make sure that all mission critical code can be compiled with any language compliant compiler, can be analyzed by a broad range of tools, and can be understood, debugged, tested, and maintained by any competent C programmer. It ensures that there is no hidden reliance on compiler or platform specific behavior that may jeopardize portability or code reuse, also They have a static source code  analyser, there must be any warning out of the code, this is called the rule of Zero warning.

That’s it i thought it’s a good idea to talk about the hidden part of this project from a geek and developer view and you know hardware without software is nothing.

Hope you enjoyed this article and feel free to leave a comment 🙂

Sources :
+ [http://en.wikipedia.org/wiki/VxWorks](http://en.wikipedia.org/wiki/VxWorks)  
+ [http://www.jpl.nasa.gov/index.html](http://www.jpl.nasa.gov/index.html)
