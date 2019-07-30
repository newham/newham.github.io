---
layout : post
title : Windows linux双系统的时间修改问题
date : 2019-07-30 19:12:17 +0800
categories : article
description : Windows linux双系统,两个系统的时间不一致，改了一边的，另一边的就会错乱，好像相差了8小时。
---

一 在Windows下进行如下修改：
在 注册表项：`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\TimeZoneInformation\`
下中添加一项数据类型为`REG_DWORD`，名称为`RealTimeIsUniversal`，值设为`1`的键值。
或者直接使用下如下批处理进行修改：
```
------------------------------------------------------------------------
@echo off
color 0a
Reg add HKLM\SYSTEM\CurrentControlSet\Control\TimeZoneInformation /v RealTimeIsUniversal /t REG_DWORD /d 1
echo.
echo 已让Windows识别存贮在主板CMOS内的时间为格林威治标准时间（GMT）,即系统根据CMOS时间和设置的时区来确定当前系统的时间。
echo.
pause
---------------------------------------------------------------------------
```
二 或者 在Ubuntu下进行如下修改： 【推荐】  
Ubuntu中不使用UTC时间，而启用本地时间，需要修改 /etc/default/rcS ，修改动作如下：  
# 注释掉原来的设定：UTC=yes  
# 变更为下面的内容...  
UTC=no  
最好在linux下的修改：  
“系统”－>“管理”—>“时间和日期”—>“时区”，把UTC的勾去掉  