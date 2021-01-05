---
title: GDI 支持服务
description: GDI 支持服务
keywords:
- GDI WDK Windows 2000 显示，服务例程
- 图形驱动程序 WDK Windows 2000 显示，服务例程
- 绘制 WDK GDI，服务例程
- 服务例程 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d297e6ce098ec57321321235d9bde4745a0afa55
ms.sourcegitcommit: abd90176b0416a1170b1c0232943b60543dd6b98
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/29/2020
ms.locfileid: "97812486"
---
# <a name="gdi-support-services"></a>GDI 支持服务

*GDI* 将导出许多可简化驱动程序设计的服务例程。 驱动程序可以直接调用这些例程。 例程的名称，这些例程的名称以 **Eng** 开头。 与特定对象相关的服务例程始终以对象的名称开头;例如， [**CLIPOBJ_cEnumStart**](/windows/win32/api/winddi/nf-winddi-clipobj_cenumstart) 是 [**CLIPOBJ**](/windows/win32/api/winddi/ns-winddi-clipobj) 服务。

**注意**   第一个参数是指向用户对象的指针是该用户对象上的方法，并且是使用常用 c + + 约定调用的服务例程。 因此，用 c + + 编写的驱动程序可以将服务例程作为方法来访问。

这些服务例程分为以下几类：

[Surface management](gdi-support-for-surfaces.md)

[调色板服务](gdi-support-for-palettes.md)

[路径服务](gdi-services-for-paths.md)

[窗口服务](gdi-support-for-window-objects.md)

[呈现服务](gdi-drawing-and-related-services.md)

[字体和文本服务](gdi-font-and-text-services.md)

[内存服务](gdi-memory-services.md)

[事件服务](gdi-event-services.md)

[文件、模块和进程服务](gdi-file--module--and-process-services.md)

[信号服务](gdi-semaphore-services.md)

[打印机服务](gdi-printer-services.md)

[与驱动程序相关的服务](gdi-driver-related-services.md)

[信息服务](gdi-information-services.md)

[实用工具服务](gdi-utility-services.md)

[浮点服务](gdi-floating-point-services.md)

[半色调服务](gdi-halftone-services.md)

[使用图形 ddi](using-the-graphics-ddi.md) 介绍图形 ddi 入口点，并说明其中许多服务例程可用于帮助驱动程序实现入口点。
