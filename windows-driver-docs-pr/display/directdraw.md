---
title: DirectDraw
description: DirectDraw
keywords:
- DirectDraw WDK Windows 2000 显示
- Windows 2000 显示器驱动程序型号 WDK，DirectDraw
- 显示驱动程序模型 WDK Windows 2000，DirectDraw
- 标头文件 WDK DirectDraw
- DirectDraw WDK Windows 2000 显示，头文件
- 绘制 WDK DirectDraw
- 绘制 WDK DirectDraw，头文件
- 图形 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 30c069243ed3d28cd18daab9ccc1bdae029ae830
ms.sourcegitcommit: e47bd7eef2c2b89e3417d7f2dceb7c03d894f3c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2020
ms.locfileid: "97091060"
---
# <a name="directdraw"></a>DirectDraw


## <span id="ddk_directdraw_gg"></span><span id="DDK_DIRECTDRAW_GG"></span>


本部分介绍 Microsoft DirectDraw 接口和体系结构，并为 DirectDraw 驱动程序编写器提供实现准则。 本指南专为 Microsoft Windows 2000 及更高版本编写。 读者应该熟悉 DirectDraw Api，并对 Windows 2000 显示器驱动程序模型进行牢固的理解。

正在为 Microsoft Windows 2000 和更高版本创建 Microsoft DirectDraw 驱动程序的驱动程序编写器应使用以下头文件：

-   *ddrawint* 包含 DirectDraw 驱动程序的基本类型、常量和结构。

-   *ddraw* 包含应用程序和驱动程序使用的基本类型、常量和结构。

-   当驱动程序 (VPE) 支持 DirectDraw 视频端口扩展时，将使用 *dvp。*

-   当视频微型端口驱动程序包括对内核模式视频传输的支持、DxApi 接口 (由 [**DxApi \_ 接口**](/windows/win32/api/dxmini/ns-dxmini-dxapi_interface)结构) 指定的函数时，将使用 *dxmini* 。

-   视频捕获驱动程序使用 *ddkmapi* 来访问 [**DxApi**](/windows-hardware/drivers/ddi/dxapi/nf-dxapi-dxapi)函数。 DirectDraw 又会调用 DxApi 接口。

-   当驱动程序要执行其自己的内存管理，而不是依赖于 DirectDraw 运行时，将使用 *dmemmgr。*

-   当驱动程序包含内核模式支持时，将使用 *ddkernel。*

-   *dx95type* 使驱动程序编写者可以轻松地将现有 windows 98/Me 驱动程序移植到 windows 2000 和更高版本。 此标头文件映射两个平台上不同的名称。

*Ddraw* 头文件随 Windows SDK 一起提供;所有其他标头文件都包含在 (WDK) 的 Windows 驱动程序工具包中。 Windows 驱动程序开发工具包 (DDK) 还在 *p3samp* 视频显示目录中包含 DirectDraw 驱动程序的示例代码。

Directdraw 驱动程序函数、回调和结构的引用页可以在 [Directdraw 驱动程序函数](/windows-hardware/drivers/ddi/_display/#functions) 和 [Directdraw 驱动程序结构](/windows-hardware/drivers/ddi/_display/#structures)中找到。

有关 DirectDraw 的详细信息，请参阅 Windows SDK。 DirectDraw 驱动程序作者可以通过电子邮件向发送问题和评论 <em>directx@microsoft.com</em> 。

 

