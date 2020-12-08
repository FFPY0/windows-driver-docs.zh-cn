---
title: 创建中断对象
description: 了解如何创建中断对象。 驱动程序可以从 "EvtDriverDeviceAdd" 和 "EvtDevicePrepareHardware" 回调函数创建中断对象。
keywords:
- 硬件中断 WDK KMDF，对象创建
- 中断 WDK KMDF，对象创建
- 消息-已发出信号中断 WDK KMDF
- Msi WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4ecb6bdeef1a229061168c65ae6db0f033e423c5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829037"
---
# <a name="creating-an-interrupt-object"></a>创建中断对象


用于处理设备硬件中断的 Windows 驱动程序框架 (WDF) 驱动程序必须为每个设备可以支持的每个中断创建一个框架中断对象。 在版本1.11 及更高版本的操作系统上运行的 framework 版本和更高版本中，Kernel-Mode Driver Framework (KMDF) 和 User-Mode Driver Framework (UMDF) 驱动程序可以创建需要 [被动级别处理的](supporting-passive-level-interrupts.md)中断对象。 但除非你要为芯片 (SoC) 平台上的系统编写驱动程序，但是，你的驱动程序应使用 DIRQL 中断对象。

驱动程序通常会在其 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 回调函数中创建框架中断对象。 驱动程序还可以从其 [*EvtDevicePrepareHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware) 回调函数创建中断对象。

在即插即用 (PnP) manager 将系统资源（如中断向量）分配给设备之前，框架将调用驱动程序的 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 回调函数。 PnP 管理器分配资源后，框架会在设备的中断对象中存储中断资源。  ([不支持即插即用](using-kernel-mode-driver-framework-with-non-pnp-drivers.md) 的驱动程序不能使用中断对象。 ) 

若要创建框架中断对象，驱动程序必须初始化 [**WDF \_ 中断 \_ 配置**](/windows-hardware/drivers/ddi/wdfinterrupt/ns-wdfinterrupt-_wdf_interrupt_config) 结构，并将其传递给 [**WdfInterruptCreate**](/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptcreate) 方法。

UMDF 支持以下类型的中断：

-   级别触发的 (共享或独占) 
-   边缘-触发的 (仅限独占) 
-   MSI (按定义进行排他) 

**注意**  UMDF 不支持 *共享* 边缘触发的中断。

 

从 UMDF 版本2.15 开始，UMDF 支持对简单设备（如硬件推送按钮，通常由 GPIO pin 提供支持）进行中断，不能使用硬件注册来显式启用或禁用。 为支持此类设备，UMDF 驱动程序必须使用独占边缘触发的中断。

从 KMDF 版本1.15 开始，KMDF 还支持此类设备的中断，而不是 [处理 Active-Both 中断](handling-active-both-interrupts.md)中介绍的解决方法。

此外，在 [**WDF \_ 中断 \_ 配置**](/windows-hardware/drivers/ddi/wdfinterrupt/ns-wdfinterrupt-_wdf_interrupt_config)中，驱动程序提供指向下列驱动程序提供的事件回调函数的指针：

<a href="" id="---------evtinterruptenable--------"></a>[*EvtInterruptEnable*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_enable)  
启用硬件中断。

<a href="" id="---------evtinterruptdisable--------"></a>[*EvtInterruptDisable*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_disable)  
禁用硬件中断。

<a href="" id="---------evtinterruptisr--------"></a>[*EvtInterruptIsr*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_isr)  
中断服务例程为中断 (ISR) 。

<a href="" id="---------evtinterruptdpc--------"></a>[*EvtInterruptDpc*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc)  
延迟过程调用 (DPC) 用于中断。

<a href="" id="evtinterruptworkitem"></a>[*EvtInterruptWorkItem*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_workitem)  
[被动级别中断](supporting-passive-level-interrupts.md)的工作项。

对于在 Windows 8 或更高版本的操作系统上使用 framework 1.11 或更高版本的驱动程序，该驱动程序可以将框架中断对象 (DIRQL 或被动) 的父对象显式设置为框架设备对象或框架队列对象。 如果驱动程序指定了父驱动程序，则驱动程序必须将中断对象的 [**WDF \_ 中断 \_ 配置**](/windows-hardware/drivers/ddi/wdfinterrupt/ns-wdfinterrupt-_wdf_interrupt_config)结构的 **AutomaticSerialization** 成员设置为 TRUE。  (回忆，如果 **AutomaticSerialization** 为 TRUE，则框架会将中断对象的 [*EvtInterruptDpc*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc) 或 [*EvtInterruptWorkItem*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_workitem) 回调函数的执行与中断父对象下的其他对象中的回调函数同步。 ) 

例如，驱动程序可能将队列指定为中断的父，以将队列的回调与中断的 [*EvtInterruptDpc*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_dpc) 或 [*EvtInterruptWorkItem*](/windows-hardware/drivers/ddi/wdfinterrupt/nc-wdfinterrupt-evt_wdf_interrupt_workitem) 回调同步。 在此配置中，框架在删除设备对象时删除队列对象。

调用 [**WdfInterruptCreate**](/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptcreate)之后，驱动程序可以选择调用 [**WdfInterruptSetPolicy**](/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptsetpolicy) 或 [**WdfInterruptSetExtendedPolicy**](/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptsetextendedpolicy) 来指定其他中断参数。 通常，驱动程序从其 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 回调函数调用这些方法。

在删除中断的父节点之前，框架会自动删除该中断。 或者，驱动程序可以调用 [**WdfObjectDelete**](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectdelete) 来删除中断。

## <a name="supporting-message-signaled-interrupts"></a>支持消息终止的中断


从 Windows Vista 开始，支持 (Msi) 的消息信号中断。 若要使操作系统支持设备的 Msi，驱动程序的 INF 文件必须在注册表中设置一些值。 有关如何设置这些值的信息，请参阅 [启用注册表中的 Message-Signaled 中断](../kernel/enabling-message-signaled-interrupts-in-the-registry.md)。

驱动程序应为设备可以支持的每个中断矢量或 MSI 消息创建框架中断对象。 如果 PnP 管理器未向设备授予设备能够支持的所有中断资源，将不会使用额外的中断对象，也不会调用其回调函数。

在 Windows 7 中，操作系统不支持每个设备的每个设备运行超过910个中断消息的资源请求。 在 Windows 8 中，操作系统不支持对每个设备功能的超过2048个中断的资源请求。

如果设备驱动程序超过此限制，则设备可能无法启动。 若要在包含多个逻辑处理器的计算机上操作，驱动程序不应为每个处理器请求多个中断。

驱动程序必须承受中断资源的系统重新平衡，其中 PnP 管理器会将中断资源的系统重新平衡，其中 PnP 管理器将任何一组备用中断资源从资源需求列表分配到该设备。 例如，可能会为设备分配比请求的驱动程序数更少的消息中断。 在最坏的情况下，驱动程序必须准备好只需一个基于线路的中断即可操作设备。

 

