---
title: 电源管理中的驱动程序角色
description: 电源管理中的驱动程序角色
keywords:
- 电源管理 WDK 内核，中的驱动程序角色
- 系统电源状态 WDK 内核，驱动程序角色
- 设备电源状态 WDK 内核
- 驱动程序电源支持角色 WDk 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3ca73cfade99357172c399d033ff1ea0747b507c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825899"
---
# <a name="driver-role-in-power-management"></a>电源管理中的驱动程序角色





驱动程序通过两种方式支持电源管理：

1.  驱动程序对由电源管理器发出的系统范围的电源请求做出响应。

2.  驱动程序管理其各个设备的电源和性能状态。

每个驱动程序都必须有一个 [*DispatchPower*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程来处理 [**IRP \_ MJ \_ 电源**](./irp-mj-power.md) 请求。 *DispatchPower* 例程必须检查每个电源 IRP，并对其进行处理或将其向下传递到下一个较低的驱动程序。

要使设备参与电源管理，设备的设备堆栈中的每个驱动程序都必须适当地响应或传递电源 Irp。 单个驱动程序无法正常运行可能会导致在整个系统中禁用电源管理。

每个设备一个驱动程序管理其设备的 [电源策略](managing-device-power-policy.md) 。 该驱动程序可以将 power Irp 发送到其自己的设备堆栈，以在其设备上执行电源操作。 电源策略管理器负责发出与系统电源 Irp 相对应的设备电源 Irp。

此外，驱动程序可能会执行某些电源任务，如在启动时打开设备，或在删除设备时关闭设备，而无需接收电源 IRP。 它们被视为隐式电源请求。

有关详细信息，请参阅 [驱动程序的电源管理责任](power-management-responsibilities-for-drivers.md)。

 

