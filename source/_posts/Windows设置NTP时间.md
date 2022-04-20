---
title: Windows设置NTP时间
date: 2021-10-09 19:03:43
tags: C++ 
categories: C++
---

- 步骤1：打开注册表，WIN+R打开搜索框，输入regedit

  ![搜索框](https://img0.baidu.com/it/u=808989156,1923249855&fm=26&fmt=auto "搜索框")

- 步骤2：打开注册表中           [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time\Config\AnnounceFlags] AnnounceFlags 值修改为5

- 步骤3：打开注册表[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\W32Time\TimeProviders\NtpServer] 将Enabled修改为：1 

- 步骤4：win+X打开管理员shell命令行 
             通过net stop w32time 停止服务
             net start w32time 启动服务
             检测命令：w32tm /stripchart /computer:ntp_server_address

- 步骤5：添加防火墙规则
  控制面板--->系统和安全--->windows防火墙--->高级设置--->入站规则（右键）--->新建规则---> 端口 ---下一步----UDP----特定本地端口：123（不要换别的）
  一直点下一步，直到下面这个页面名称：NTP，完成；

- 步骤6：开机自启动
                打开服务
                设置windows Time服务属性为自动

