---
title: 显示驱动程序（Windows 2000 模型）
description: 显示驱动程序（Windows 2000 模型）
keywords:
- 显示驱动程序模型 WDK Windows 2000，显示驱动程序
- Windows 2000 显示器驱动程序模型 WDK，显示驱动程序
- 显示驱动程序 WDK Windows 2000
- 显示驱动程序 WDK Windows 2000，关于显示器驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 39a8078b7ae2c842cd486a08b028c5c1133655d9
ms.sourcegitcommit: abd90176b0416a1170b1c0232943b60543dd6b98
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/29/2020
ms.locfileid: "97812591"
---
# <a name="display-drivers-windows-2000-model"></a>显示驱动程序（Windows 2000 模型）

基于 Microsoft NT 的操作系统显示驱动程序编写器涉及两个核心软件接口：

- 图形 DDI 接口-显示驱动程序实现的函数集。 GDI 可以调用图形 DDI 接口来处理图形命令。

- GDI 接口-系统提供的、由显示驱动程序调用的帮助器例程，以简化驱动程序实现。

本部分介绍与基于 NT 的操作系统显示驱动程序相关的关键概念，以及一些实现信息。 有关打印机驱动程序和显示驱动程序（如驱动程序初始化和终止）和图形输出等常见的图形驱动程序设计细节，请参阅 [对图形驱动程序的 GDI 支持](gdi-support-for-graphics-drivers.md) 和 [使用图形 DDI](using-the-graphics-ddi.md) 。

显示驱动程序编写器还可以实现以下 DDIs：

- DirectDraw DDI-图形接口，允许供应商提供适用于 DirectDraw 的硬件加速。 有关详细信息，请参阅 [DirectDraw](directdraw.md) 。

- Direct3D DDI-三维图形界面，允许供应商提供 Direct3D 的硬件加速。 有关详细信息，请参阅 [DIRECT3D DDI](direct3d.md) 。
