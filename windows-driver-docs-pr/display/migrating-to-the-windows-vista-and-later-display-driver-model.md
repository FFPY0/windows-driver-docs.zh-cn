---
title: 迁移到 Windows 显示驱动程序模型 (WDDM)
description: 迁移到 Windows 显示驱动程序模型 (WDDM)
keywords:
- 显示驱动程序模型 WDK Windows Vista，迁移
- Windows Vista 显示器驱动程序模型 WDK，迁移
- 迁移显示器驱动程序模型 WDK Windows Vista
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 76472f5c24ce0704e16ff94bf1586c87690302a1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822455"
---
# <a name="migrating-to-the-windows-display-driver-model-wddm"></a>迁移到 Windows 显示驱动程序模型 (WDDM)


## <span id="ddk_migrating_to_the_longhorn_display_driver_model_gg"></span><span id="DDK_MIGRATING_TO_THE_LONGHORN_DISPLAY_DRIVER_MODEL_GG"></span>


迁移到 Windows 显示驱动程序模型 (WDDM) # A2 需要驱动程序编写器来编写完全不同的显示和视频微型端口驱动程序。 类似于 [Windows 2000 显示器驱动程序模型 (XDDM) ](windows-2000-display-driver-model-design-guide.md)，WDDM 要求成对显示驱动程序并显示微型端口驱动程序。 但在 WDDM 中，显示驱动程序在用户模式下运行。 此外，该模型不会使用 Windows 图形设备接口的服务 (GDI) 引擎;该模型使用 Microsoft Direct3D 运行时的服务和 Microsoft DirectX 图形内核子系统 ( # A0) 。

WDDM 支持根据 XDDM 编写的显示和视频微型端口驱动程序。 但是，应尽可能将新驱动程序编写为 WDDM 驱动程序，以利用从 Windows Vista 开始提供的软件和硬件功能。

尽管驱动程序编写器可以在其 WDDM 驱动程序中重复使用低级别硬件相关代码，但它们应该重写新的设备驱动程序接口 (与 DDI) 相关的代码。 编写 WDDMdrivers 时，请注意以下几点：

-   显示微型端口驱动程序必须实现一组修改后的入口点函数，使其与操作系统和 DirectX 图形内核子系统交互。 有关详细信息，请参阅 [**DriverEntry Of 显示微型端口驱动程序**](./driverentry-of-display-miniport-driver.md)。 显示微型端口驱动程序可以调用任何记录的内核函数。

-   显示微型端口驱动程序动态加载相应的 DirectX 图形内核子系统。 显示微型端口驱动程序和 DirectX 图形内核子系统通过接口相互调用。

-    (IOCTL) ，无需再处理显示微型端口驱动程序。 在 XDDM 中，内核模式显示驱动程序使用以下代码与视频微型端口驱动程序通信。 在 WDDM 中，用户模式显示驱动程序与 Direct3D 运行时通信;WDDM 图形内核子系统又与显示微型端口驱动程序通信。
    **注意**  以下 IOCTLs 仍用于 WDDM，显示微型端口驱动程序必须处理它们： [**ioctl \_ 视频 \_ 查询 \_ 颜色 \_ 功能**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_query_color_capabilities) 
     [**ioctl \_ 视频 \_ 句柄 \_ VIDEOPARAMETERS**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_handle_videoparameters)

     

<!-- -->

-   用户模式显示驱动程序必须实现和导出 [**OpenAdapter**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_openadapter) 函数，该函数将打开图形适配器的实例。 用户模式显示驱动程序还必须实现一个 [**CreateDevice**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createdevice) 函数，该函数可创建显示设备的表示形式，这些表示处理呈现状态的集合。

-   用户模式显示驱动程序的 [**CreateResource**](/windows-hardware/drivers/ddi/d3dumddi/nc-d3dumddi-pfnd3dddi_createresource) 函数，以及显示微型端口驱动程序的 [**DxgkDdiCreateAllocation**](/windows-hardware/drivers/ddi/d3dkmddi/nc-d3dkmddi-dxgkddi_createallocation) 函数，替换 D3dCreateSurfaceEx 中的 [*DdCanCreateSurface*](/previous-versions/windows/hardware/drivers/ff549213(v=vs.85))、 [*DdCreateSurface*](/previous-versions/windows/hardware/drivers/ff549263(v=vs.85))和 [**XDDM**](/windows/win32/api/ddrawint/nc-ddrawint-pdd_createsurfaceex) 函数。

-   大多数其余的用户模式显示驱动程序函数实现的功能与 XDDM 的内核模式显示驱动程序实现的功能相同：
    -   [**D3dDrawPrimitives2**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb)函数和 [**DP2**](/windows-hardware/drivers/ddi/d3dhal/ne-d3dhal-_d3dhal_dp2operation)操作代码
    -   [运动补偿回调函数](/windows-hardware/drivers/ddi/index)和[DirectX 视频加速结构](/windows-hardware/drivers/ddi/index)

 

