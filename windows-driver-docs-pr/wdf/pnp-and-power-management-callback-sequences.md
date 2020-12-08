---
title: PnP 和电源管理回调序列
description: 以下主题显示了框架调用 WDF 驱动程序的 PnP 和电源管理事件回调函数的顺序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 245d4ef1a37858bba3abe0985564a6b2f79a2194
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795773"
---
# <a name="pnp-and-power-management-callback-sequences"></a>PnP 和电源管理回调序列


以下主题显示了框架调用 WDF (KMDF 和 UMDF v2) 驱动程序的 PnP 和电源管理事件回调函数的顺序：

-   [函数或筛选器驱动程序的启动顺序](power-up-sequence-for-a-function-or-filter-driver.md)
-   [总线驱动程序的启动顺序](power-up-sequence-for-a-bus-driver.md)
-   [函数或筛选器驱动程序的电源关闭和删除顺序](power-down-and-removal-sequence-for-a-function-or-filter-driver.md)
-   [总线驱动程序的电源关闭和删除顺序](power-down-and-removal-sequence-for-a-bus-driver.md)
-   [意外删除顺序](surprise-removal-sequence.md)
-   [WDM Irp 和相应的 WDF 事件回调](./wdm-irps-and-kmdf-event-callback-functions.md)

以下主题标识典型的 PnP 和电源管理方案，并显示在这些情况下框架调用驱动程序的事件回调函数的顺序：

- [用户插入设备](a-user-plugs-in-a-device.md)
- [用户拔出设备](a-user-unplugs-a-device.md)
- [设备进入低功耗状态](a-device-enters-a-low-power-state.md)
- [设备回到工作状态](a-device-returns-to-its-working-state.md)
- [PnP 管理器重新分发系统资源](the-pnp-manager-redistributes-system-resources.md)
 

