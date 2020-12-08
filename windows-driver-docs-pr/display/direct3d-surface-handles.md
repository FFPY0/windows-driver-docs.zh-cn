---
title: Direct3D 图面句柄
description: Direct3D 图面句柄
keywords:
- 上下文 WDK Direct3D，surface 控点
- surface 处理 WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f916e3f286860c9e68461bee35ca7904432794d0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809443"
---
# <a name="direct3d-surface-handles"></a>Direct3D 图面句柄


## <span id="ddk_direct3d_surface_handles_gg"></span><span id="DDK_DIRECT3D_SURFACE_HANDLES_GG"></span>


Microsoft DirectX 7.0 设备驱动程序接口 (DDI) 旨在促进这样一种模型：在将命令传递给驱动程序之前，Direct3D 运行时组件分析尽可能少的命令流。 此外，应对命令流设置格式，使其可供将来的硬件使用。

针对这些目标的一项重要变化是，从 Direct3D/DirectDraw 运行时所拥有的中间结构的所有表面相关数据移到由驱动程序拥有、更新和格式化的结构。

在命令流中嵌入的句柄引用了表面。 在这些高频操作中，驱动程序可以在图面上查找自己的图面表示形式，而无需通过 helper 函数（如 [**EngLockDirectDrawSurface**](/windows/win32/api/winddi/nf-winddi-englockdirectdrawsurface)）锁定曲面。

分配这些句柄的机制是名为 " [**D3dCreateSurfaceEx**](/windows/win32/api/ddrawint/nc-ddrawint-pdd_createsurfaceex)" 的驱动程序入口点。 此入口点在调用现有的 [*DdCanCreateSurface*](/previous-versions/windows/hardware/drivers/ff549213(v=vs.85)) 和 [*DdCreateSurface*](/previous-versions/windows/hardware/drivers/ff549263(v=vs.85)) 入口点之后，以及在视频内存地址和句柄已分配给表面之后直接调用。 在 **D3dCreateSurfaceEx** 时，驱动程序将所有相关信息从 DirectDraw 运行时的 surface 结构副本复制到其自身的 surface 结构。 驱动程序端副本对于诸如大小、格式和 **fpVidMem** 之类的图面 [**\_ 图面图面 \_**](/windows/win32/api/ddrawint/ns-ddrawint-dd_surface_global) 结构) 的成员 (是必需的。

对于每个设备和每个进程，句柄都保证是唯一的。 句柄对于每个上下文都是唯一的，因此，在 [创建 Driver-Side Surface 结构](creating-driver-side-surface-structures.md)时更详细地讨论了驱动程序的某些含义。

没有相应的 **DestroySurfaceEx** 调用，因此驱动程序端表面结构在 [*DdDestroySurface*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_surfcb_destroysurface) 时被销毁。

 

