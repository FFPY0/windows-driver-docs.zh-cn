---
title: 回顾旧式对齐方法
description: 回顾旧式对齐方法
keywords:
- 绘制扩展图面对齐 WDK DirectDraw
- DirectDraw 扩展图面对齐 WDK Windows 2000 显示器
- surface DirectDraw，扩展对齐
- 扩展的图面对齐 WDK DirectDraw
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: daeb25421b736c83b473c953ddf6b359ae3803fc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831861"
---
# <a name="review-of-the-older-alignment-method"></a>回顾旧式对齐方法


## <span id="ddk_review_of_the_older_alignment_method_gg"></span><span id="DDK_REVIEW_OF_THE_OLDER_ALIGNMENT_METHOD_GG"></span>


DirectX 5.0 之前的 DirectDraw 版本允许驱动程序为线性堆提供快速调整对齐要求。 出于此讨论的目的，可以通过以下三个步骤来查看 DirectDraw 的这些对齐要求：

1.  基于驱动程序的全局对齐要求，创建图面并填充对齐的 **lPitch** 成员， (如 [**VIDEOMEMORYINFO**](/windows/win32/api/ddrawint/ns-ddrawint-videomemoryinfo) 结构中所返回的一样) 和图面的 **ddsCaps** 成员。 此跨度将增加，直到它是适当的对齐要求的倍数。

2.  如果已定义，则调用驱动程序的 [*DdCreateSurface*](/previous-versions/windows/hardware/drivers/ff549263(v=vs.85)) 回调。 驱动程序可以修改 **lPitch** 值，但 Microsoft Windows 2000 和更高版本将忽略此更改。

3.  如果未处理驱动程序调用，或请求分配，则从驱动程序的一个堆中为表面分配显示内存。 除非步骤2中的驱动程序进行了修改，否则分配的表面的宽度将是在步骤1中确定的对齐间距。

如果驱动程序实现了 [*DdCreateSurface*](/previous-versions/windows/hardware/drivers/ff549263(v=vs.85)) 回调，则可以确保所有传入表面都将其 **lPitch** 成员设置为对齐值。 为了向后兼容，此行为仍然存在。 第三步保持完全相同的行为，除非驱动程序公开了 **GetHeapAlignment** 入口点 (请参阅 [**DD \_ GETHEAPALIGNMENTDATA**](/windows/win32/api/dmemmgr/ns-dmemmgr-dd_getheapalignmentdata) 结构) 。 如果且仅当定义了此入口点后，将放弃之前计算出的 **lPitch** 对齐方式，所有表面对齐都符合使用 GUID GetHeapAlignment 报告的需求 \_ 。 驱动程序可以保持其 [**VIDEOMEMORYINFO**](/windows/win32/api/ddrawint/ns-ddrawint-videomemoryinfo) 结构的对齐要求，并在较旧的 DirectDraw 运行时上运行时，预期的对齐方式也是相同的。 已完全为 DirectX 5.0 和更高版本的 DirectDraw 运行时版本替换此对齐方式。 应注意的是，公开 **GetHeapAlignment** 会关闭所有堆的此旧对齐过程，而不只是 GUID \_ GetHeapAlignment 报告对齐要求的情况。

 

