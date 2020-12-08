---
title: 通过类安装程序和辅助安装程序修改注册表项
description: 通过类安装程序和辅助安装程序修改注册表项
keywords:
- 注册表 WDK 设备安装，修改注册表项
- 注册表 WDK 设备安装，修改注册表项，类安装程序
- 注册表 WDK 设备安装，修改注册表项，共同安装程序
- 类安装程序 WDK 设备安装，修改注册表项
- 共同安装程序 WDK 设备安装，修改注册表项
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b54d740677bb7873b7706e10a66f7fbfd95b13a7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827630"
---
# <a name="modifying-registry-keys-by-class-installers-and-co-installers"></a>通过类安装程序和辅助安装程序修改注册表项


**注意**  通用或移动驱动程序包不支持本部分中介绍的功能。 请参阅 [使用通用 INF 文件](using-a-universal-inf-file.md)。

 

除非在某些情况下， *类安装* 程序和 *共同安装程序* 不应使用标准注册表函数来创建、更改或删除注册表项。 在大多数情况下，只能使用放在 [INF 文件](overview-of-inf-files.md)中的指令来修改注册表项。 有关这些指令的详细信息，请参阅 [INF 指令摘要](summary-of-inf-directives.md)。

下面是此规则的例外情况：

-   必要时，类安装程序和共同安装程序可以使用标准注册表功能修改 **HKLM \\ 软件** 子树中的注册表项。

    **注意**  我们强烈建议类安装程序和共同安装程序将自定义设备属性保存为设备的 *软件密钥* 中的条目。

     

-   允许类安装程序和共同安装程序修改 **HKLM \\ System \\ CurrentControlSet \\ Control \\ CoDeviceInstallers** 注册表项中的子项。

应遵循以下准则，以安全地修改类安装程序或共同安装程序的注册表项：

-   类安装程序和共同安装程序必须首先使用 [**SetupDiCreateDevRegKey**](/windows/win32/api/setupapi/nf-setupapi-setupdicreatedevregkeya) 或 [**SetupDiOpenDevRegKey**](/windows/win32/api/setupapi/nf-setupapi-setupdiopendevregkey) 来打开要修改的注册表项的句柄。 打开句柄后，类安装程序和共同安装程序可以使用标准注册表函数来修改注册表项。

-   类安装程序和共同安装程序不得使用 [**SetupDiDeleteDevRegKey**](/windows/win32/api/setupapi/nf-setupapi-setupdideletedevregkey) 来删除设备的 *软件密钥* 或 *硬件密钥* 。 有关详细信息，请参阅 [删除设备的注册表项](deleting-the-registry-keys-of-a-device.md)。

有关标准注册表函数的详细信息，请参阅 [注册表函数](/windows/win32/sysinfo/registry-functions)。

