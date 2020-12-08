---
title: 线程同步和 TDR
description: 线程同步和 TDR
keywords:
- 线程 WDK 显示，TDR
- 同步 WDK 显示，TDR
- TDR (超时检测和恢复) WDK 显示和线程同步
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 580904673b9e9f4d873acbafc713942da2760f32
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830043"
---
# <a name="thread-synchronization-and-tdr"></a>线程同步和 TDR

下图显示了在 Windows 显示驱动程序模型 (WDDM) 中，线程同步如何适用于显示微型端口驱动程序。

![阐释 windows vista 线程同步的关系图](images/lddmsync.png)

如果发生硬件超时， [TDR) 进程 (会启动超时检测和恢复 ](timeout-detection-and-recovery.md) 。 GPU 计划程序将调用驱动程序的 [*DxgkDdiResetFromTimeout*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_resetfromtimeout) 函数，该函数将重置 GPU。 *DxgkDdiResetFromTimeout* 与任何其他显示微型端口驱动程序函数同步调用，而运行时电源管理功能 [*DxgkDdiSetPowerComponentFState*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddisetpowercomponentfstate) 和 [*DxgkDdiPowerRuntimeControlRequest*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddipowerruntimecontrolrequest)除外。 也就是说，当 *DxgkDdiResetFromTimeout* 线程运行时，驱动程序中不会运行任何其他线程。 操作系统还保证在调用 *DxgkDdiResetFromTimeout* 期间，不能从任何应用程序访问帧缓冲区。因此，驱动程序可以重置内存控制器阶段锁定循环 (PLL) 等。

当恢复线程执行 [*DxgkDdiResetFromTimeout*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_resetfromtimeout)时，可以继续调用 (dpc) 的中断和延迟过程调用。 [**KeSynchronizeExecution**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesynchronizeexecution)函数可用于通过设备中断来同步重置过程的部分。

驱动程序从 [*DxgkDdiResetFromTimeout*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_resetfromtimeout)返回后，可以再次调用大多数驱动程序函数，操作系统会开始清理不再需要的资源。 在清理期间，出于以下原因，将调用以下驱动程序函数：

- 调用该驱动程序，通知即将逐出分配。

  例如，如果分配在内存段中分页，则会调用驱动程序的 [*DxgkDdiBuildPagingBuffer*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer)函数，并将 [**DXGKARG_BUILDPAGINGBUFFER**](/windows-hardware/drivers/ddi/d3dkmddi/ns-d3dkmddi-_dxgkarg_buildpagingbuffer)结构集的 **Operation** 成员设置为 DXGK_OPERATION_TRANSFER 并将 **传输. Size** 成员设置为零，以通知驱动程序逐出。 请注意，不涉及任何内容传输，因为内容在重置过程中丢失。

  如果分配在口径段内分页，则会调用驱动程序的 [*DxgkDdiBuildPagingBuffer*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_buildpagingbuffer) 函数，并将 DXGKARG_BUILDPAGINGBUFFER 设置为 DXGK_OPERATION_UNMAP_APERTURE_SEGMENT 的 **操作** 成员通知驱动程序将分配从口径取消映射。

- 调用驱动程序的 [*DxgkDdiReleaseSwizzlingRange*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_releaseswizzlingrange) 函数以释放 unswizzling 口径和分段口径范围。

除非绝对必要，否则驱动程序不能在前面的调用期间访问 GPU。

清除时间段结束后，操作系统将调用驱动程序的 [*DxgkDdiRestartFromTimeout*](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_restartfromtimeout) 函数，以通知驱动程序清理已完成，并且操作系统将使用适配器进行呈现。
