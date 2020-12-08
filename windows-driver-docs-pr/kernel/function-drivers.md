---
title: 函数驱动程序
description: 函数驱动程序
keywords:
- 函数驱动程序 WDK WDM
- raw 模式 WDK WDM
- WDM 函数驱动程序 WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: f273419dcec2c4421423828244f663612dead77a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839067"
---
# <a name="function-drivers"></a>函数驱动程序





*函数驱动程序* 是设备的主驱动程序 (查看可能的 [驱动层](types-of-wdm-drivers.md#possible-driver-layers)) 。 函数驱动程序通常由设备供应商编写，并 (，除非该设备正在 *raw 模式*) 使用。 PnP 管理器最多为一个设备加载一个函数驱动程序。 函数驱动程序可以为一个或多个设备服务。

函数驱动程序为其设备提供操作接口。 通常，函数驱动程序处理对设备的读取和写入操作，并管理设备电源策略。

设备的函数驱动程序可以实现为驱动程序/微型驱动程序对，例如端口/微型端口驱动程序对或 class/miniclass 驱动程序对。 在此类驱动程序对中，微型驱动程序链接到第二个驱动程序，该驱动程序是一个 DLL。

如果设备在 raw 模式下驱动，则它没有函数驱动程序，且没有上层或较低级别的筛选器驱动程序。 所有 raw 模式 i/o 都是通过总线驱动程序和可选的总线筛选器驱动程序来完成的。

 

 




