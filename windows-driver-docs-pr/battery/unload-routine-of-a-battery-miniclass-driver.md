---
title: 电池微型类驱动程序的 Unload 例程
description: 电池微型类驱动程序的 Unload 例程
keywords:
- 电池 miniclass 驱动程序 WDK，例程
- 卸载例程
- 验证设备卸载
- 卸载设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e6e761374ab1f5c04e86651213b435fe68b066b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798655"
---
# <a name="unload-routine-of-a-battery-miniclass-driver"></a>电池微型类驱动程序的 Unload 例程


## <span id="ddk_unload_routine_of_battery_miniclass_driver_dg"></span><span id="DDK_UNLOAD_ROUTINE_OF_BATTERY_MINICLASS_DRIVER_DG"></span>


电池 miniclass 驱动程序的 *卸载* 例程可确保已删除所有驱动程序的设备并释放 miniclass 驱动程序已分配的所有资源。

*卸载* 例程应该首先检查以确保所有设备已被删除，如果不是，请为其余每个设备执行以下操作：

1.  调用 [**BatteryClassUnload**](/windows/win32/api/batclass/nf-batclass-batteryclassunload) 以通知类驱动程序，miniclass 驱动程序正在卸载设备。

2.  使用该驱动程序的接口，从较低的驱动程序（如 ACPI 驱动程序）禁用任何设备通知。

3.  通过调用 [**IoDeleteDevice**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iodeletedevice)删除设备的设备对象，如下所示：

    ```cpp
        IoDeleteDevice (NewBatt->DeviceObject);
    ```

卸载所有 miniclass 驱动程序的设备后， *卸载* 例程应释放由 miniclass 驱动程序分配的所有资源。

删除所有驱动程序的设备后，可以随时调用 miniclass 驱动程序的 *Unload* 例程。 PnP 管理器在系统线程的上下文中以 IRQL = 被动级别调用 *卸载* 例程 \_ 。

 

