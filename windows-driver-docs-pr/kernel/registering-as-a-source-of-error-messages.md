---
title: 注册为错误消息的源
description: 注册为错误消息的源
keywords:
- 源注册 WDK 错误
- 错误 WDK 内核
- 正在注册错误消息源
- 注册表 WDK 错误日志
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 786e00b743a21acfd756fe6573b825ca37667ba1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837707"
---
# <a name="registering-as-a-source-of-error-messages"></a>注册为错误消息的源





驱动程序在注册表中注册错误消息源。 驱动程序必须在 **HKEY \_ LOCAL \_ MACHINE \\ system \\ CurrentControlSet \\ service \\ EventLog \\ \\ system**<em>DriverName</em>下设置两个密钥：

<a href="" id="eventmessagefile--reg-expand-sz-"></a>**EventMessageFile** (REG \_ 展开 \_ SZ)   
用分号分隔的错误消息源的列表。 如果驱动程序使用标准错误类型，则此列表必须包括 iologmsg.dll。 如果驱动程序使用附加到驱动程序映像的错误消息，则必须包含驱动程序映像的名称。

<a href="" id="typessupported--reg-dword-"></a>**TypesSupported** (REG \_ DWORD)   
可以记录的可能严重级别的位掩码。 驱动程序通常将此设置为7，以指示它们可能会记录所有严重性级别。

有关如何从驱动程序的 INF 文件设置这些注册表项的说明，请参阅 [**注册事件日志记录**](../install/inf-addservice-directive.md)。

 

