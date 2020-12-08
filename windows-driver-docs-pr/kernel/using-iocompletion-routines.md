---
title: 使用 IoCompletion 例程
description: 使用 IoCompletion 例程
keywords:
- IoCompletion 例程
- 完成 Irp WDK 内核，IoCompletion 例程
- 完成 Irp WDK 内核，调度例程
- 调度例程 WDK 内核，完成 Irp
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d736ad99fa77e7ca605dba74c3a7602614e4d929
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814229"
---
# <a name="using-iocompletion-routines"></a>使用 IoCompletion 例程





针对特定于 IRP 的驱动程序，可监视特定于 IRP 的驱动程序执行特定请求的方式如何有一个或多个 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程。 分配 Irp 以将请求发送到较低驱动程序的高级驱动程序必须具有 *IoCompletion* 例程。

最高级别或中间驱动程序的 [*DispatchRead*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 或 [*DispatchWrite*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程最有可能为 IRP 设置 *IoCompletion* 例程，因为较低级别的驱动程序必须异步处理传输请求。

驱动程序堆栈中的最低级别驱动程序无法注册 *IoCompletion* 例程。

通常，驱动程序不会为与同步 i/o 操作关联的 Irp 注册 *IoCompletion* 例程。 例如，更高级别的驱动程序的 [*DispatchDeviceControl*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程可以使用 [**IoBuildDeviceIoControlRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)分配 IRP。 在这种情况下，调度例程通常不会注册 *IoCompletion* 例程，因为通常同步处理设备控制请求。 相反，驱动程序可以分配和初始化事件对象，其 *DispatchDeviceControl* 例程可以等待事件在发送到驱动程序分配的 irp 上时进行初始化。 通常，较高级别的驱动程序不会为使用 [**IoBuildSynchronousFsdRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuildsynchronousfsdrequest)分配的 IRP 注册 *IoCompletion* 例程，因为同样的原因。

本节包含下列主题：

[注册 IoCompletion 例程](registering-an-iocompletion-routine.md)

[实现 IoCompletion 例程](implementing-an-iocompletion-routine.md)

 

