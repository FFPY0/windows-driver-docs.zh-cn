---
title: INF DDInstall.MigrateToDevNode 节
description: INF DDInstall.MigrateToDevNode 节
keywords:
- INF 文件 WDK 非 HID 键盘/鼠标
- DDInstall. MigrateToDevNode 部分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 817253af138e8cbce4e716ebfe2341535ed836e4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838043"
---
# <a name="inf-ddinstallmigratetodevnode-section"></a>INF DDInstall.MigrateToDevNode 节

\[**<em>安装--name</em>**。MigrateToDevNode- \] \[ **<em>name</em>**。MigrateToDevNode \] \[ **<em>install-section-name</em>**. ntx86。MigrateToDevNode \] \[ **<em>install-section-name</em>**. ntia64。MigrateToDevNode\]

<em>ServiceName</em> **=**<em>值-名称</em> \[**，**<em>值-name</em> \] ,.。。键盘和鼠标类安装程序将 *值名称* 字符串列表指定的条目值从注册表项 **HKLM \\ System \\ CurrentControlSet \\ Services \\**<em>ServiceName</em>**\\ 参数** 复制到要安装的设备的设备节点。

## <a name="entries-and-values"></a>项和值

<a href="" id="servicename"></a>*ServiceName*  
指定与设备端口关联的服务名称 (例如， **i8042prt**、 **sermouse** 等) 。

<a href="" id="value-name"></a>*值-名称*  
指定注册表项 **HKLM \\ System \\ CurrentControlSet \\ Services \\**<em>ServiceName</em>**\\ 参数** 下的条目值。

## <a name="remarks"></a>备注

Microsoft 支持 INF <em>DDinstall</em>**。MigratetoDevNode** 部分主要用于帮助将 WINDOWS NT 4.0 旧设备移植到 windows 2000 及更高版本。

键盘和鼠标类安装程序会在系统启动设备堆栈之前复制所有 *值名称* 条目值。 指定的条目值可以是任何有效的注册表项值。 不会从中 **\\** 删除 *值-name* 条目值。<em>ServiceName</em>**\\ 参数** 注册表项。
