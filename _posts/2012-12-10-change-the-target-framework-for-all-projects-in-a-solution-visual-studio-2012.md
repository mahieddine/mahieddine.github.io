---
layout: post
title:  "Change the Target Framework for all Projects in a Solution (Visual Studio 2012)"
date:   2012-12-10 20:00:23 +0700
categories: [dotnet]
---
If you installed VS 2012 and you are a big fan of Macros you’ve certainly noted that there is no macro support in VS 2012, one of the main reasons exposed by Microsoft Team is the fastidious and hard work necessary to maintain this old thing working with the new version of visual studio and also to push developers developing their own add-ins. the fact is that developing adding take an amount of time that most of the time a simple developper doesn’t have and want simply to code a fast automated task simply and quickly. So i’m a little upset about this…

The main reason i’m writing this article is that at work i was in front of a big deal which is migrating my solution (which contains over 70 projects) to .net framework 4.5, so i had those choices :

1. Migrate project one by one 🙂
2. Develop an add-in (i don’t have enough time for this)
3. Develop my custom macro which i did
4. So you can simply download my macro [Macro Change TargetFramework](/static/files/upload/project-utilities.zip)
5. To use my macro you have to follow this steps :
6. Open your solution under VS 2010 (Yes you need visual studio 2010 just to execute the  Macro)
7. Run the Macro
8. Put in the prompt Fx45
9. Then open your solution again under vs 2012 (and Checkin  eventually in your source control system)

That’s it

