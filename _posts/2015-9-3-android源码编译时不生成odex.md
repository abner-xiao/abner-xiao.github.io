---
layout:	post
title:	"android源码编译时不生成odex"
date:	2015-09-03 23:30:00
categories:	android
---

###android源码编译时不生成odex
在对应包的Android.mk文件中添加LOCAL_DEX_PREOPT := false即可