---
layout:	post
title:	"解决Android源码环境下编译Luncher3报错"
date:	2015-09-03 23:30:00
categories:	android
---

###解决Android源码环境下编译Luncher3报错
今天下载android4.4源码，依照官方的操作编译成功，然后本来想着修改下Launcher3玩玩的,结果cd到Launcher3执行mm竟然报错了，提示如下：

“make: *** 没有规则可以创建“out/target/common/obj/APPS/Launcher3_intermediates/classes-full-debug.jar”需要的目标“out/target/common/obj/JAVA_LIBRARIES/libprotobuf-java-2.3.0-nano_intermediates/javalib.jar”。 停止。”

于是上网查找资料，原来是Launcher3依赖的host-libprotobuf-java-2.3.0-nano.jar包没有编译进去，于是通过mma编译当前目录下所有的模块以及这些模块所依赖的模块即可解决。