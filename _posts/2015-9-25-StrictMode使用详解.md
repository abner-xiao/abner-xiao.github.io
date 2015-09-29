---
layout:	post
title:	StrictMode使用详解
date:	2015-09-25 21:49:45
categories:	android
---

##StrictMode使用详解
1、线程策略(和线程相关，主要是主线程相关)

`StrictMode.setThreadPolicy(new StrictMode.ThreadPolicy.Builder()
                    .detectDiskReads()
                    .detectDiskWrites()
                    .detectNetwork()   // or .detectAll() for all detectable problems
                    .penaltyLog()      //将警告输出到logcat
                    .build());
`

2、虚拟机策略(可以检查内存泄露)

`StrictMode.setVmPolicy(new StrictMode.VmPolicy.Builder()
                    .detectLeakedSqlLiteObjects()
                    .detectLeakedClosableObjects()
                    .penaltyLog()
                    .penaltyDeath()
                    .build());`