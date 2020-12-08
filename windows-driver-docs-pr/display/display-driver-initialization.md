---
title: 显示驱动程序初始化
description: 显示驱动程序初始化
keywords:
- 显示驱动程序 WDK Windows 2000，初始化
- 初始化显示驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 482ecbdd24089591728cd48ffb36c163c79411c2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809281"
---
# <a name="display-driver-initialization"></a>显示驱动程序初始化

如 [支持初始化和终止功能](supporting-initialization-and-termination-functions.md)中所述，显示器驱动程序初始化类似于图形驱动程序初始化。 本节提供特定于显示驱动程序的初始化详细信息。

在加载和初始化 NT executive 和 Win32 子系统后，会发生视频微型端口和显示驱动程序初始化。 系统会加载视频微型端口驱动程序或在注册表中启用的驱动程序，然后确定要使用的视频微型端口驱动程序和显示驱动程序对。 在此过程中，GDI 将根据窗口管理器提供的信息打开所有必需的显示驱动程序。

下图显示了基本的显示驱动程序初始化过程，其中创建了桌面。

![显示驱动程序初始化说明的示意图](images/202-01.png)

1. 在调用 GDI 以便为视频硬件创建第一个设备上下文 (*DC*) 时，gdi 将调用显示驱动程序函数 [**DrvEnableDriver**](/windows/win32/api/winddi/nf-winddi-drvenabledriver)。 返回时， **DrvEnableDriver** 提供了一个 [**DRVENABLEDATA**](/windows/win32/api/winddi/ns-winddi-drvenabledata) 结构的 GDI，该结构保存驱动程序的图形 ddi 版本号和驱动 (程序实现的所有可调用图形 ddi 函数的入口点，而不是 **DrvEnableDriver**) 。

2. 然后，GDI 将调用驱动程序的 [**DrvEnablePDEV**](/windows/win32/api/winddi/nf-winddi-drvenablepdev) 函数来请求驱动程序的物理设备特征的说明。 在调用中，GDI 会传入 [**DEVMODEW**](/windows/win32/api/wingdi/ns-wingdi-devmodew) 结构，该结构标识 gdi 要设置的模式。 如果 GDI 请求显示或基础微型端口驱动程序不支持的模式，则显示驱动程序必须无法通过此调用。

3. 显示驱动程序表示由 GDI 控制的逻辑设备。 如下图中所示，单个逻辑设备可以管理多个物理设备，每种设备都以硬件类型、逻辑地址和支持的表面为特征。 显示驱动程序分配内存以支持它创建的设备。 可以调用显示驱动程序来管理同一个物理设备上的多个 *PDEV* ，但对于给定的物理设备，一次只能启用一个 PDEV。 每个 PDEV 都是在对 [**DrvEnablePDEV**](/windows/win32/api/winddi/nf-winddi-drvenablepdev)的单独 GDI 调用中创建的，并且每个调用会创建另一个与不同的表面一起使用的 PDEV。

   由于驱动程序必须支持多个 PDEV，因此它不应使用全局变量。

   调用 [**DrvEnableSurface**](/windows/win32/api/winddi/nf-winddi-drvenablesurface)后，GDI 会自动启用 DirectDraw。 初始化 DirectDraw 后，驱动程序可以使用 DirectDraw 的 *堆管理器* 来执行 *屏幕外内存* 管理。 有关详细信息，请参阅 [DirectDraw 和 GDI](directdraw-and-gdi.md) 。

   下图显示了逻辑与物理设备。

   ![阐释逻辑设备与物理设备的示意图](images/202-03.png)

4. 物理设备安装完成后，GDI 将调用 [**DrvCompletePDEV**](/windows/win32/api/winddi/nf-winddi-drvcompletepdev)。 此函数为驱动程序提供了一个 GDI 生成的物理设备句柄，以便在为设备请求 GDI 函数时使用。

5. 在初始化的最后阶段，会通过对 [**DrvEnableSurface**](/windows/win32/api/winddi/nf-winddi-drvenablesurface)的 GDI 调用为视频硬件创建一个表面，使图形输出到硬件。 根据设备和环境，显示驱动程序可通过以下两种方式之一启用图面：

   * 驱动程序通过调用 GDI 函数 **EngCreateDeviceSurface** 方法来管理其自己的图面：对于不支持标准格式位图的硬件，此方法是必需的，对于具有的硬件，它是可选的。
   * 如果硬件设备具有组织为标准格式位图的图面，则 GDI 可以完全将其视为 *引擎管理的图* 面。 驱动程序可以调用 [**EngModifySurface**](/windows/win32/api/winddi/nf-winddi-engmodifysurface) 将 *设备管理* 的主位图转换为 *引擎管理* 的主位图。 驱动程序仍可以挂钩任何绘图操作。

任何现有的 GDI 位图句柄都是有效的图面控点。 驱动程序可以调用 [**EngModifySurface**](/windows/win32/api/winddi/nf-winddi-engmodifysurface) 将设备管理的主位图转换为引擎托管的位图。 如果该图面由引擎管理，则 GDI 可以处理任何或所有绘图操作。 如果图面是设备托管的，则驱动程序必须至少处理 [**DrvTextOut**](/windows/win32/api/winddi/nf-winddi-drvtextout)、 [**DrvStrokePath**](/windows/win32/api/winddi/nf-winddi-drvstrokepath)和 [**DrvBitBlt**](/windows/win32/api/winddi/nf-winddi-drvbitblt)。

调用 [**DrvEnableSurface**](/windows/win32/api/winddi/nf-winddi-drvenablesurface)后，GDI 会自动启用 DirectDraw。 初始化 DirectDraw 后，驱动程序可以使用 DirectDraw 的 *堆管理器* 来执行 [*屏幕外内存*](video-present-network-terminology.md#off_screen_memory) 管理。 有关详细信息，请参阅 [DirectDraw 和 GDI](directdraw-and-gdi.md) 。

显示驱动程序必须实现 [**DrvNotify**](/windows/win32/api/winddi/nf-winddi-drvnotify) 才能接收通知事件，特别是 DN_DRAWING_BEGIN 事件。 GDI 在开始绘制之前立即发送此事件，因此它可用于确定缓存何时可以初始化。

有关启动过程的详细信息，请参阅 " [即插即用](../kernel/introduction-to-plug-and-play.md) " 部分。
