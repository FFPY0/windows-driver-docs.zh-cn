---
title: 识别画笔
description: 识别画笔
keywords:
- GDI WDK Windows 2000 显示，模式
- 图形驱动程序 WDK Windows 2000 显示，模式
- 模式 WDK GDI
- 画笔 WDK GDI
- 刷子原点 WDK GDI
- 实现画笔 WDK GDI
- 抖动 WDK Windows 2000 显示
- 颜色抖动 WDK Windows 2000 显示
- 颜色管理 WDK GDI
- DrvRealizeBrush
- DrvDitherColor
- 表面画笔图案 WDK GDI
- 填充 WDK GDI
- 线条 WDK GDI
- 绘制 WDK GDI，画笔
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84c55de8177cb724a77bdca7f469e39d3687b62b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810085"
---
# <a name="realizing-brushes"></a>识别画笔

## <a name="how-to-realize-a-brush"></a>如何实现画笔

输出线条、文本或填充的图形函数至少采用一个画笔作为参数。 画笔定义用于在指定图面上绘制图形对象的模式。 采用画笔的每个输出函数都需要一个 *画笔原点*。 画笔原点提供设备图面上的像素坐标，使其与画笔图案的左上角像素对齐。 画笔模式 (平铺) ，以覆盖整个设备表面。

驱动程序可以支持以下函数来定义画笔：

* [**DrvRealizeBrush**](/windows/win32/api/winddi/nf-winddi-drvrealizebrush)
* [**DrvDitherColor**](/windows/win32/api/winddi/nf-winddi-drvdithercolor)

画笔始终与混合模式结合使用，用于定义应如何将模式与设备图面上已有的数据混合使用。 组合数据类型包含两个打包为一个 ULONG 值的 ROP2 值。 前景 *ROP* 为最低序位字节。 下一个字节包含后台 ROP。 有关详细信息，请参阅 Microsoft Windows SDK 文档。

GDI 跟踪应用程序请求使用的所有逻辑画笔。 在要求驱动程序绘制东西之前，GDI 首先发出对驱动程序函数 [**DrvRealizeBrush**](/windows/win32/api/winddi/nf-winddi-drvrealizebrush)的调用。 这使得驱动程序可以为其自己的绘制代码计算所需模式的最佳表示形式。

调用 *DrvRealizeBrush* ，以实现) 画笔的 *psoPattern* (模式定义的画笔，并通过 *psoTarget* (表面实现已实现的画笔) 。 已实现的画笔包含驱动程序需要使用模式填充区域的信息和加速器。 此信息仅由驱动程序定义和使用。 画笔的驱动程序实现被写入缓冲区，该缓冲区可通过调用 *DrvRealizeBrush* 中的 GDI 服务函数 [**BRUSHOBJ_pvAllocRbrush**](/windows/win32/api/winddi/nf-winddi-brushobj_pvallocrbrush)来分配驱动程序。 GDI 将缓存所有已实现的画笔;因此，很少需要重新计算。

在 *DrvRealizeBrush* 中， [**BRUSHOBJ**](/windows/win32/api/winddi/ns-winddi-brushobj) 用户对象表示画笔。 要实现画笔的图面可以是设备的物理表面、 *DDB* 或标准格式的位图。 对于光栅设备，描述画笔模式的图面表示位图;对于向量设备，它始终是 [**DrvEnablePDEV**](/windows/win32/api/winddi/nf-winddi-drvenablepdev) 函数返回的模式图面中的一个。 画笔使用的透明度掩码是一位每像素位图，其范围与模式相同。 掩码位为零表示像素被视为画笔的背景像素;也就是说，目标像素不受该特定模式像素的影响。 *DrvRealizeBrush* 使用 [**XLATEOBJ**](/windows/win32/api/winddi/ns-winddi-xlateobj) 结构将画笔模式中的颜色转换为设备颜色索引。

当 BRUSHOBJ 结构的 **iSolidColor** 成员的值为0Xffffffff 并且 **PvRbrush** 成员为 **NULL** 时，驱动程序应调用 GDI 服务 [**BRUSHOBJ_pvGetRbrush**](/windows/win32/api/winddi/nf-winddi-brushobj_pvgetrbrush)函数。 **BRUSHOBJ_pvGetRbrush** 检索指向指定画笔的驱动程序实现的指针。 如果当驱动程序调用此函数时未实现画笔，则 GDI 会自动为驱动程序实现画笔而调用 *DrvRealizeBrush* 。

## <a name="dithering"></a>抖动

如有必要，在尝试使用无法完全在硬件上表示的纯色创建画笔时，GDI 可以请求驱动程序的帮助。 GDI 调用驱动程序函数 [**DrvDitherColor**](/windows/win32/api/winddi/nf-winddi-drvdithercolor) 来请求驱动程序根据 *设备调色板* 的保留部分来仿色画笔。

抖动使用多种颜色的模式来接近所选颜色，其结果是设备颜色索引的数组。 使用这些颜色为其模式创建的画笔通常是给定颜色的理想近似值。 [**DrvDitherColor**](/windows/win32/api/winddi/nf-winddi-drvdithercolor) 也可以表示不能由设备精确指定的颜色。 为此， *DrvDitherColor* 请求多种颜色的模式并创建一个接近给定纯色的画笔。

函数 *DrvDitherColor* 是可选的，仅当在 [**Lnk-devinfo**](/windows/win32/api/winddi/ns-winddi-devinfo)结构的 **flGraphicsCaps** 成员中设置 GCAPS_COLOR_DITHER 或 GCAPS_MONO_DITHER 功能标志时才会调用。 *DrvDitherColor* 可以返回下表中列出的值。

| “值” | 含义 |
| ----- | ------- |
| DCR_DRIVER | 指示已由驱动程序计算仿色值。 在这种情况下，将向后传递设备颜色索引的 **cxDither** by **cyDither** 数组的句柄。 |
| DCR_HALFTONE | 指示 GDI 应使用现有设备 (半色调) 调色板来近似颜色。 例如，GDI 可以为仅包含三种或四种颜色的打印机使用典型的调色板。 仅当设备包含设备 (半色调) 调色板（如 VGA-16 适配器卡，它具有标准固定调色板）时，DCR_HALFTONE 才可与显示器驱动程序一起使用。 |
| DCR_SOLID | 指示 GDI 应将请求的颜色映射到现有设备调色板中最接近的颜色值 (多个) 。 |

单色驱动程序应支持 *DrvDitherColor* ，以便 GDI 获取良好的灰色级别的模式。
