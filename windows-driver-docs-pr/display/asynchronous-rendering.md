---
title: 异步渲染
description: 异步渲染
keywords:
- 显示驱动程序 WDK Windows 2000，异步呈现
- 异步呈现 WDK Windows 2000 显示
- 以异步方式呈现 WDK Windows 2000 显示器
- 同步 WDK Windows 2000 显示
- 批处理 DirectDraw 绘图调用 WDK Windows 2000 显示
- DirectDraw WDK Windows 2000 显示，调用批处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 133f30ead1b107c93ed6f7ff726d405b88bae0dc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810479"
---
# <a name="asynchronous-rendering"></a>异步渲染

用于处理一个或多个图形 DDI 绘图操作的显示驱动程序通过使用 [**EngModifySurface**](/windows/win32/api/winddi/nf-winddi-engmodifysurface)来异步提供对其位图的 GDI 访问。 驱动程序还必须提供同步例程，以避免在批处理图形 DDI 绘图操作时绘制错误。

此类驱动程序可以选择实现其中一个 [**DrvSynchronizeSurface**](/windows/win32/api/winddi/nf-winddi-drvsynchronizesurface) 或 [**DrvSynchronize**](/windows/win32/api/winddi/nf-winddi-drvsynchronize) 作为同步例程。 GDI 仅当驱动程序在 [**EngAssociateSurface**](/windows/win32/api/winddi/nf-winddi-engassociatesurface)中挂接它们时才调用其中一个例程。 GDI 将仅在挂接了这两个同步例程的驱动程序中调用 **DrvSynchronizeSurface** 。

[**DrvSynchronizeSurface**](/windows/win32/api/winddi/nf-winddi-drvsynchronizesurface) 向驱动程序提供有关同步事件的其他信息及其出现的原因。 这使得驱动程序可以减少由于同步导致的性能延迟。 例如，如果指定的表面目前不在队列中，则跟踪哪些设备位图位于加速器的队列中的驱动程序可能能够立即返回 **DrvSynchronizeSurface** 。

除了提供同步例程以外，驱动程序还可以通过在 [**lnk-devinfo**](/windows/win32/api/winddi/ns-winddi-devinfo)结构的 **flGraphicsCaps2** 字段中设置以下标志来激活 *基于时间* 或 *编程* 的刷新机制：

* GCAPS2_SYNCTIMER：设置此标志将导致定期调用驱动程序的同步例程。 批处理图形 DDI 调用的驱动程序必须指定此标志。 通过这样做，这些驱动程序可避免出现一些问题，如软件游标移动或在突发中执行的绘图中的 lag。

  当由于定期事件而调用此同步例程时，GDI 将 DSS_TIMER_EVENT 标志传递到 [**DrvSynchronizeSurface**](/windows/win32/api/winddi/nf-winddi-drvsynchronizesurface) 。

* GCAPS2_SYNCFLUSH：设置此标志会导致在调用 Microsoft Win32 **GdiFlush** API 时调用驱动程序的同步例程。 执行异步呈现的驱动程序必须指定此标志并提供同步例程。

  由于基于刷新的事件而调用此同步例程时，GDI 将 DSS_FLUSH_EVENT 标志传递到 [**DrvSynchronizeSurface**](/windows/win32/api/winddi/nf-winddi-drvsynchronizesurface) 。 有关 **GdiFlush** 的详细信息，请参阅 Microsoft Windows SDK 文档。

> [!NOTE]
> 当目标图面为可见屏幕时，驱动程序不得批处理 DirectDraw 绘图调用。 这种情况发生在有窗口的 DirectX 应用程序中，其中已完成的框架通过 [*DdBlt*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_surfcb_blt) 更新到屏幕，因此应该立即显示。 此限制也适用于 DirectDraw 视频端口图面，它们可能会以异步方式翻转。
