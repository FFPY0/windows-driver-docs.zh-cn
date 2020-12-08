---
title: GDI 与驱动程序的通信
description: GDI 与驱动程序的通信
keywords:
- GDI WDK Windows 2000 显示器，驱动程序通信
- 图形驱动程序 WDK Windows 2000 显示器、驱动程序通信
- 绘制 WDK GDI，驱动程序通信
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c5151c63ae6822620e0ddec81eb4e04882de12b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837801"
---
# <a name="gdi-communication-with-the-driver"></a>GDI 与驱动程序的通信


## <span id="ddk_gdi_communication_with_the_driver_gg"></span><span id="DDK_GDI_COMMUNICATION_WITH_THE_DRIVER_GG"></span>


驱动程序仅将一个函数导出到 GDI： [**DrvEnableDriver**](/windows/win32/api/winddi/nf-winddi-drvenabledriver)。 所有其他支持驱动程序的函数（包括 [**DrvDisableDriver**](/windows/win32/api/winddi/nf-winddi-drvdisabledriver) 函数）通过指针数组向 GDI 公开。 对 **DrvEnableDriver** 的 GDI 调用将初始化驱动程序并传递回驱动程序支持的图形 DDI 函数的列表。 虽然驱动程序必须支持一些函数，但 GDI 将处理从驱动程序的 **DrvEnableDriver** 例程收到的函数列表中不包含的操作。 当驱动程序要卸载时，GDI 将调用 *DrvDisableDriver* 。 有关图形 DDI 函数的详细讨论，请参见 [使用图形 ddi](using-the-graphics-ddi.md)。

GDI 使大量的对象和服务可供驱动程序使用。 它们分为两类：用户对象和服务例程。

 

