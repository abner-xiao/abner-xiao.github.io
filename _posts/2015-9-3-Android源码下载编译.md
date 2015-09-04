---
layout:	post
title:	"Android源码下载编译"
date:	2015-09-03 23:30:00
categories:	android
---

##Android源码下载编译

####1、下载安装Repo

`$ mkdir ~/bin`
`$ PATH=~/bin:$PATH`
`$ curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo`
`$ chmod a+x ~/bin/repo`
 由于防火墙的缘故，repo的下载需要翻墙，或者通过一下方式下载：
 `git clone git://aosp.tuna.tsinghua.edu.cn/android/git-repo.git/`

####2、初始化Repo
`$ mkdir WORKING_DIRECTORY`
`$ cd WORKING_DIRECTORY`
`$ repo init -u https://android.googlesource.com/platform/manifest`//master分支
如果需要下载指定分支的源码则通过一下命令初始化：
`$ repo init -u https://android.googlesource.com/platform/manifest -b android-4.4.4_r2`
然后会提示配置名称和邮箱，可以在Repo初始化之前通过：
`$ git config --global user.name "name"`
`$ git config --global user.email "email"`
提前进行名称和邮箱的配置

<!--more-->

####3、下载源码
`$ repo sync`
这个过程就只有漫长的等待了，当然网速快就好很多了
###4、编译源码
`$ source build/envsetup.sh`
或者
`$ . build/envsetup.sh`
选择需要编译的target
`$ lunch aosp_arm-eng`
可以直接运行`lunch`在输出列表中选择需要编译的target
最后执行：
`make -j4`//需要根据你的CPU来指定参数，直接make默认为单线程
####5、运行
`$ emulator`
直接启动模拟器运行刚才编译好的android系统

######依然由于防火墙的原因，山gia你涉及到的`https://android.googlesource.com/`是无法连接上的，好在我们可以通过如下方法进行替代：
将`https://android.googlesource.com/`更换为`git://aosp.tuna.tsinghua.edu.cn/android/`
同时打开repo进行如下修改：
` <remote  name="aosp"
       fetch=".."
       review="https://android-review.googlesource.com/" />`
改为下面的code即可： 
` <remote  name="aosp"
 fetch="git://aosp.tuna.tsinghua.edu.cn/android/"
 review="https://android-review.googlesource.com/" />`