---
title: 有关编写 DPC 例程的指导原则
description: 有关编写 DPC 例程的指导原则
keywords:
- 延迟的过程调用 WDK 内核
- Dpc WDK 内核
- DpcForIsr
- CustomDpc
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4e41619e7d91c23766d425485ce3028d9e06fb1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790517"
---
# <a name="guidelines-for-writing-dpc-routines"></a>有关编写 DPC 例程的指导原则





编写 [*DpcForIsr*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_dpc_routine) 或 [*CustomDpc*](/windows-hardware/drivers/ddi/wdm/nc-wdm-kdeferred_routine) 例程时，请记住以下几点：

-   *DpcForIsr* 或 *CustomDpc* 例程必须将其访问权限同步到物理设备、驱动程序维护的任何共享状态信息或资源，以及访问同一设备或内存位置的驱动程序的其他例程。

    如果 *DpcForIsr* 或 *CUSTOMDPC* 例程与 ISR 共享设备或状态，则它必须调用 [**KeSynchronizeExecution**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution)，提供驱动程序提供的、用于计划设备或访问共享状态的 [*SynchCritSection*](/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine) 例程的地址。 有关详细信息，请参阅 [使用关键部分](using-critical-sections.md)。

    如果 " *DpcForIsr* " 或 " *CustomDpc* " 例程共享状态或资源（例如联锁队列或计时器对象，而不是 ISR 除外），则它必须使用驱动程序初始化的执行旋转锁来保护共享状态或资源。 有关详细信息，请参阅 [自旋锁](./introduction-to-spin-locks.md)。

-   *DpcForIsr* 和 *CUSTOMDPC* 例程以 IRQL = 调度 \_ 级别运行，这会限制它们可调用的支持例程集。

    例如， *DpcForIsr* 和 *CustomDpc* 例程既无法访问也不分配可分页内存，并且它们无法等待将 [内核调度程序对象](./introduction-to-kernel-dispatcher-objects.md) 设置为已终止状态。 另一方面，他们可以使用 [**KeAcquireSpinLockAtDpcLevel**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlockatdpclevel) 和 [**KeReleaseSpinLockFromDpcLevel**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlockfromdpclevel)获取和释放驱动程序的 executive 旋转锁，这比 **KeAcquireSpinLock** 和 **KeReleaseSpinLock** 运行得更快。

    尽管 DPC 例程无法进行阻止调用，但它可以将工作项排队，使其在以 IRQL = 被动级别运行的 [系统工作线程](system-worker-threads.md) 中运行 \_ 。 工作项可以发出等待调度程序对象的阻止调用。 若要将工作项排队， *DpcForIsr* 例程通常会调用例程（如 [**IoQueueWorkItem**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioqueueworkitem)），而 *CustomDpc* 例程通常会调用 [**ExQueueWorkItem**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exqueueworkitem) 例程。

-   *DpcForIsr* 和 *CustomDpc* 例程通常负责在设备上启动下一次 i/o 操作。

    对于使用直接 i/o 的最低级别物理设备驱动程序，这种责任可以包括使用 [*SynchCritSection*](/windows-hardware/drivers/ddi/wdm/nc-wdm-ksynchronize_routine) 例程来对设备进行编程，以便在驱动程序调用 [**IoStartNextPacket**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iostartnextpacket)之前，满足当前 IRP 的要求。

-   *DpcForIsr* 和 *CustomDpc* 例程只应运行一小段时间，并将尽可能多的处理委托给工作线程。

    当 DPC 例程在处理器上运行时，会阻止所有线程在同一处理器上运行。 在当前 DPC 例程结束之前，已排队且可运行的其他 DPC 例程可以被阻止执行。 为避免降级系统响应能力，每次调用一个典型的 DPC 例程时，其运行时间不会超过100微秒。 如果任务需要超过100微秒，并且必须以 IRQL = 调度级别执行 \_ ，则 DPC 例程应在100微秒后结束，并计划一个或多个 [*CustomTimerDpc*](https://msdn.microsoft.com/library/windows/hardware/ff542983) 例程以便以后完成该任务。 有关 *CustomTimerDpc* 例程的详细信息，请参阅 [Timer 对象和 dpc](timer-objects-and-dpcs.md)。

    DPC 例程只应执行必须在调度级别运行的任务 \_ ，然后将任何剩余中断相关的工作委托给在 IRQL = 被动级别运行的线程 \_ 。 例如，DPC 例程可将工作项排队，使其在 [系统工作线程](system-worker-threads.md)中运行。

    调用 [**KeStallExecutionProcessor**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-kestallexecutionprocessor) 例程以延迟执行的 DPC 例程不得指定超过100毫秒的延迟。

    使用 WDK 中的性能分析工具来评估 DPC 例程的执行时间。 有关使用 [Tracelog](../devtest/tracelog.md) 工具监视 dpc 执行时间的示例，请参阅 [示例15：度量 Dpc/ISR Time](../devtest/example-15--measuring-dpc-isr-time.md)。

-   如果驱动程序使用 DMA 并且其 [*AdapterControl*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_control) 例程返回 **KeepObject** 或 **DeallocateObjectKeepRegisters** (从而为其他传输操作保留系统 DMA 控制器通道或主线主机适配器) ，则 *DpcForIsr* 或 *CustomDpc* 例程负责释放适配器对象，或在完成当前 IRP 并返回控制权之前，先将其映射到 [**FreeAdapterChannel**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_adapter_channel) 或 [**FreeMapRegisters**](/windows-hardware/drivers/ddi/wdm/nc-wdm-pfree_map_registers) 。

-   如果最低级别的物理设备驱动程序设置 [控制器对象](./introduction-to-controller-objects.md) ，以便通过控制器将 i/o 操作同步到连接的设备，则其 *DpcForIsr* 或 *CustomDpc* 例程负责在完成当前 IRP 并返回控制权之前，使用 [**IoFreeController**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-iofreecontroller) 释放控制器对象。

-   *DpcForIsr* 和 *CustomDpc* 例程通常负责记录处理给定请求期间发生的任何设备错误、在必要时重试当前请求，以及设置 i/o 状态块并为当前 IRP 调用 [**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) 。

-   如果驱动程序和设备支持重叠的 i/o 操作，则驱动程序必须遵循用于 [处理重叠 i/o 操作](handling-overlapped-i-o-operations.md)的规则。

-   任何驱动程序的 *DpcForIsr* 或 *CustomDpc* 例程通常只为驱动程序必须支持的公共 i/o 控制代码子集完成 i/o 处理。 特别是，DPC 例程完成了具有以下特征的设备控制请求操作：
    -   更改物理设备状态的请求
    -   要求返回有关物理设备的固有可变信息的请求

 

