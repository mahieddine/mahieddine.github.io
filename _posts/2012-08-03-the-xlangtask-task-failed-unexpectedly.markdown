---
layout: post
title:  "The “XLangTask” task failed unexpectedly"
date:   2012-08-03 20:00:23 +0700
categories: [eai]
---
I recently got this error while i was trying to simply compile my orchestration projet so what i’ve done is i tried to change the project target, plateforme, and i got again and again the same error even with an empty new orchestration.

> Error 2The “XLangTask” task failed unexpectedly.
> System.Runtime.InteropServices.COMException (0x80040154): Retrieving the COM class factory for component with
> CLSID {1BBA9F19-D4CC-34AA-918C-44FEF11E8274} failed due to the following error: 80040154 Class not registered (Exception from HRESULT: 0x80040154 (REGDB_E_CLASSNOTREG)).
> at Microsoft.VisualStudio.BizTalkProject.Compiler.XLangCompiler.Compile
> (BizTalkBuildSnapshot buildSnapshot, IEnumerable`1 orchestrationFilesToCompile, String switches, String outputPath, List`1& generatedCodeFiles)
> at Microsoft.VisualStudio.BizTalkProject.BuildTasks.XLangTask.Execute()
> at Microsoft.Build.BackEnd.TaskExecutionHost.Microsoft.Build.BackEnd.ITaskExecutionHost.Execute()
> at Microsoft.Build.BackEnd.TaskBuilder.ExecuteInstantiatedTask(ITaskExecutionHost taskExecutionHost,
> TaskLoggingContext taskLoggingContext, TaskHost taskHost, ItemBucket bucket, TaskExecutionMode howToExecuteTask, Boolean& taskResult)
> JMB.Ocean.Common.BatchTransfer.Orchestrations

So i decided to repair BizTalk Server on my developement machine and it worked !
Hope you find this helpful and win some time
