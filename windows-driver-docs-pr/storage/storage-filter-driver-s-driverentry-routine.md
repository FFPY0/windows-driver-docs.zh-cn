---
title: 存储筛选器驱动程序的 DriverEntry 例程
description: 存储筛选器驱动程序的 DriverEntry 例程
keywords:
- 存储筛选器驱动程序 WDK，DriverEntry
- 筛选器驱动程序 WDK 存储，DriverEntry
- SFD WDK 存储，DriverEntry
- DriverEntry WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d1de9fcd091d7ce9fa7c155590658dfa2bd1fe5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834975"
---
# <a name="storage-filter-drivers-driverentry-routine"></a>存储筛选器驱动程序的 DriverEntry 例程


## <span id="ddk_storage_filter_drivers_driverentry_routine_kg"></span><span id="DDK_STORAGE_FILTER_DRIVERS_DRIVERENTRY_ROUTINE_KG"></span>


与任何其他内核模式驱动程序一样，存储筛选器驱动程序的 [*DriverEntry*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 例程 (SFD) 必须在输入驱动程序对象中定义其调度和其他入口点。 如有必要，SFD 可以通过调用 [**IoAllocateDriverObjectExtension**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocatedriverobjectextension)分配适当大小的驱动程序对象扩展，将输入注册表路径复制到驱动程序扩展以供将来使用，并使用其他驱动程序确定的数据初始化驱动程序扩展（如果有）。

有关 PnP 驱动程序的 [*DriverEntry*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 例程的详细信息，请参阅 [即插即用](../kernel/introduction-to-plug-and-play.md)。

