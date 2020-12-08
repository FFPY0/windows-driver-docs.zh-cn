---
title: 内核调度程序对象简介
description: 内核调度程序对象简介
keywords:
- 内核调度程序对象 WDK，关于内核调度程序对象
- 调度程序对象 WDK 内核，关于内核调度程序对象
- 等待状态 WDK 内核
- 终止状态 WDK 内核
- Not-Signaled 状态 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd8e787f172a9e9d492dd40a8bb8c4d3882d1761
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825869"
---
# <a name="introduction-to-kernel-dispatcher-objects"></a>内核调度程序对象简介





内核定义一组称为 *内核调度程序对象* 的对象类型，或仅定义 *调度程序对象*。 调度程序对象包括 timer 对象、事件对象、信号量对象、互斥体对象和线程对象。

驱动程序可以在 nonarbitrary 线程上下文中使用发送器对象作为同步机制，同时在 IRQL 被动 \_ 级别执行。

### <a name="dispatcher-object-states"></a>调度程序对象状态

每个内核定义的调度程序对象类型都有一个状态设置为 "已终止" 或设置为 "无信号"。

如果一个或多个线程调用 [**KeWaitForSingleObject**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitforsingleobject)、 [**KeWaitForMutexObject**](https://msdn.microsoft.com/library/windows/hardware/ff553344)或 [**KeWaitForMultipleObjects**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kewaitformultipleobjects)，则一组线程可以同步其操作。 这些函数将发送器对象指针作为输入并等待，直到另一个例程或线程将一个或多个调度程序对象设置为终止状态。

当线程调用 **KeWaitForSingleObject** 来等待互斥) 的调度程序对象 (或 **KeWaitForMutexObject** 时，该线程会置于 *等待* 状态，直到调度程序对象设置为终止状态。 线程可以调用 **KeWaitForMultipleObjects** 来等待一组要设置为已发出信号的调度程序对象的任何或全部。

只要调度程序对象设置为 "已终止" 状态，内核就会将等待该对象的任何线程的状态更改为 " *就绪*"。  (同步计时器和同步事件是此规则的例外情况;当同步事件或计时器发出信号时，只有一个等待线程设置为 "就绪" 状态。 有关详细信息，请参阅 [计时器对象和 dpc](timer-objects-and-dpcs.md) 和 [事件对象](event-objects.md)) 。在就绪状态下，将计划根据当前运行时 [线程优先级](thread-priorities.md) 运行线程，并为具有该优先级的任何线程提供当前的处理器可用性。

### <a name="when-can-drivers-wait-for-dispatcher-objects"></a>何时驱动程序可以等待调度程序对象？

通常情况下，只有在下列情况中至少有一个条件为真时，驱动程序才能等待设置调度程序对象：

-   驱动程序在 nonarbitrary 线程上下文中执行。

    也就是说，您可以确定将进入等待状态的线程。 在实际操作中，在 nonarbitrary 线程上下文中执行的唯一驱动程序例程是任何驱动程序的 [**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)、 [*AddDevice*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)、重新 [*初始化*](/windows-hardware/drivers/ddi/ntddk/nc-ntddk-driver_reinitialize)和 [*卸载*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_unload) 例程，还是最高级别的驱动程序的调度例程。 所有这些例程直接由系统调用。

-   驱动程序正在执行完全同步的 i/o 请求。

    也就是说，任何驱动程序在处理 i/o 请求时都不会对任何操作进行排队，并且在其下的驱动程序处理完请求之前，不会返回驱动程序。

此外，如果驱动程序的执行时间为或更高，则该驱动程序不能进入等待状态 \_ 。

根据这些限制，必须使用以下规则：

-   任何驱动程序的 **DriverEntry**、 *AddDevice*、重新 *初始化* 和 *卸载* 例程都可以等待调度程序对象。

-   最高层驱动程序的调度例程可以等待调度程序对象。

-   如果 i/o 操作是同步的（如创建、刷新、关闭和关闭操作、某些设备 i/o 控制操作以及某些 PnP 和电源操作），则较低级别驱动程序的调度例程可以等待调度对象。

-   较低级别驱动程序的调度例程无法等待调度程序对象完成异步 i/o 操作。

-   在 IRQL 调度级别或更高版本上执行的驱动程序例程 \_ 不得等待调度程序对象设置为终止状态。

-   驱动程序不能尝试等待调度程序对象设置为已完成到寻呼设备的传输操作的终止状态。

-   为读取/写入请求提供服务的驱动程序调度例程通常无法等待调度程序对象设置为终止状态。

-   如果 i/o 控制代码的传输类型是缓冲方法，则设备 i/o 控制请求的调度例程可以等待调度程序对象设置为已终止状态 \_ 。

-   SCSI 微型端口驱动程序不应使用内核调度程序对象。 SCSI 微型端口驱动程序只应调用 [Scsi 端口库例程](/windows-hardware/drivers/ddi/index)。

每个其他标准驱动程序例程都在任意线程上下文中执行：调用驱动程序例程来处理排队操作或处理设备中断时，任何线程都是最新的。 而且，大多数标准驱动程序例程在调度 \_ 级别或设备驱动程序的 DIRQL 上以引发的 IRQL 运行。

如有必要，驱动程序可以创建一个设备专用线程，该线程可以等待除 ISR 或 [*SynchCritSection*](/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine) 例程以外的其他 (例程) 将调度程序对象设置为终止状态并重置为 Not-Signaled 状态。

一般原则是，如果你希望新设备驱动程序在 i/o 操作过程中等待设备状态更改时，通常需要延迟超过50微秒，请考虑使用设备专用线程实现驱动程序。 如果设备驱动程序也是最高级别的驱动程序，请考虑使用 [系统工作线程](system-worker-threads.md) 并实现一个或多个工作线程回调例程。 请参阅 [**PsCreateSystemThread**](/windows-hardware/drivers/ddi/wdm/nf-wdm-pscreatesystemthread) 和 [使用 Driver-Created 线程管理联锁队列](managing-interlocked-queues-with-a-driver-created-thread.md)。

 

