---
title: 软件优先安装
description: 软件优先安装
keywords:
- 安装应用程序 WDK，软件优先安装
- 设备安装应用程序 WDK，软件优先安装
- 分发媒体 WDK 设备安装，软件优先安装
- 软件-首次安装 WDK 设备
- 启用自动安装的安装应用程序 WDK
- 设备安装 WDK，类型
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8046b1ce3b3d4e3c0f11434e541ab6317c63f749
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806227"
---
# <a name="software-first-installation"></a>软件优先安装


在插入硬件设备之前，软件优先安装涉及系统上 [驱动程序包](driver-packages.md) 的过渡和预安装。 设备接通电源后，将从驱动程序包中安装驱动程序。

如果用户在插入设备前插入分布介质，则启用自动启动的安装应用程序可以：

-   [检查正在进行的安装](checking-for-in-progress-installations.md)，如果其他安装活动正在进行，则停止执行。

-   [确定设备是否已插入](determining-whether-a-device-is-plugged-in.md)。

-   [预安装驱动程序包](preinstalling-driver-packages.md)

-   使用 Microsoft 安装程序 [安装特定于设备的应用程序](installing-device-specific-applications.md)。

-   如果设备处于 "热插拔" 状态，请告知用户将其插入。

    如果总线未提供热插拔通知，请通过调用 [**CM_Reenumerate_DevNode**](/windows/win32/api/cfgmgr32/nf-cfgmgr32-cm_reenumerate_devnode)来启动 reenumeration。

-   如果设备无法进行热插拔，请告知用户关闭系统，插入设备，然后重新打开系统。

 

