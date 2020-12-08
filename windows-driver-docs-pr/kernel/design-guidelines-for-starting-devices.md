---
title: 启动设备的设计指导原则
description: 启动设备的设计指导原则
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4ed784189e85354f1d1773d47a4954e46f5cc161
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803549"
---
# <a name="design-guidelines-for-starting-devices"></a>启动设备的设计指导原则





-   PnP 管理器无法创建设备请求，直到 [**IRP \_ MN \_ 启动 \_ 设备**](./irp-mn-start-device.md) irp 完成，指出设备的所有驱动程序都已执行启动操作。

-   由于 [*DispatchPnP*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程在具有 IRQL 被动级别的系统线程的上下文中运行 \_ ，因此，只要驱动程序不控制包含系统页文件的设备，则在初始化过程中使用 [**ExAllocatePoolWithTag**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag) 分配的任何内存都可以从分页的池中使用。 在 *DispatchPnP* 例程返回 control 之前，必须使用 [**ExFreePool**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)释放此类内存分配。

-   WDM 设备驱动程序的 ISR 应该能够确定是否已通过虚假中断来调用它，即使在设备启动期间也是如此。 当在处理 **IRP \_ MN \_ START \_ 设备** 的代码路径中调用 [**IoConnectInterrupt**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioconnectinterrupt)时，如果在设备上启用了中断，则可以立即调用 ISR。

 

