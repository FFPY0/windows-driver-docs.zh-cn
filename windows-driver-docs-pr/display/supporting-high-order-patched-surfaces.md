---
title: 支持高阶修补图面
description: 支持高阶修补图面
keywords:
- 高阶修补的图面 WDK DirectX 9。0
- 置换映射 WDK DirectX 9。0
- 自适应镶嵌渲染状态 WDK DirectX 9。0
- 镶嵌映射 WDK DirectX 9。0
- 修补的图面 WDK DirectX 9。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a80599491892889e1541e098df541e640769c28b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793855"
---
# <a name="supporting-high-order-patched-surfaces"></a>支持高阶修补图面


## <span id="ddk_supporting_high_order_patched_surfaces_gg"></span><span id="DDK_SUPPORTING_HIGH_ORDER_PATCHED_SURFACES_GG"></span>


支持高顺序的已修补表面支持自适应分割和置换映射的设备的 DirectX 9.0 版本驱动程序必须使用功能位指示此类支持，并能够处理新的自适应镶嵌呈现状态和置换地图纹理阶段状态。 有关自适应分割和置换映射的详细信息，请参阅最新的 DirectX SDK。

为了指示支持自适应分割和置换映射，驱动程序在 D3DCAPS9 结构的 **DevCaps2** 成员中设置了以下功能位：

<span id="D3DDEVCAPS2_ADAPTIVETESSRTPATCH"></span><span id="d3ddevcaps2_adaptivetessrtpatch"></span>D3DDEVCAPS2 \_ ADAPTIVETESSRTPATCH  
设备可自适应进行分割呈现器目标修补程序。

<span id="D3DDEVCAPS2_ADAPTIVETESSNPATCH"></span><span id="d3ddevcaps2_adaptivetessnpatch"></span>D3DDEVCAPS2 \_ ADAPTIVETESSNPATCH  
设备可自适应进行分割 N-修补程序。

<span id="D3DDEVCAPS2_DMAPNPATCH"></span><span id="d3ddevcaps2_dmapnpatch"></span>D3DDEVCAPS2 \_ DMAPNPATCH  
设备支持 N 修补程序的置换地图。

<span id="D3DDEVCAPS2_PRESAMPLEDDMAPNPATCH"></span><span id="d3ddevcaps2_presampleddmapnpatch"></span>D3DDEVCAPS2 \_ PRESAMPLEDDMAPNPATCH  
设备支持 N 修补程序的 presampled 置换地图。

为了指明显示设备可以支持的 N 修补程序细分的最大数目，驱动程序将 D3DCAPS9 结构的 **MaxNpatchTessellationLevel** 成员设置为最大数目。 使用 presampled 置换映射的应用程序会受到设备钳位到此最大数目的影响。

驱动程序将返回 D3DCAPS9 结构，以响应 **GetDriverInfo2** 查询，如 [报告 DirectX 8.0 Style Direct3D 功能](reporting-directx-8-0-style-direct3d-capabilities.md)中所述的那样返回 D3DCAPS8 结构。 支持 [GetDriverInfo2](supporting-getdriverinfo2.md)中介绍了此查询的支持。

驱动程序在 \_ \_ [**DDPIXELFORMAT**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddpixelformat)结构的 **dwOperations** 成员中指定 D3DFORMAT OP DMAP 标志，该标志用于标记置换图采样格式的特定表面格式。 创建纹理图面时，Direct3D 运行时会将 \_ DDSCAPSEX ([**DDSCAPS2**](/previous-versions/windows/hardware/drivers/ff550292(v=vs.85))) 结构的 **dwCaps3** 成员的 DDSCAPS3 DMAP 位设置为，以指示可以在镶嵌单元中对纹理进行采样。

请注意，仅当 D3DRS \_ PATCHSEGMENTS 呈现状态的值小于 1.0 f 时，DirectX 9.0 和更高版本的驱动程序才能关闭 N 修补程序功能。 DirectX 8.1 和更早版本的驱动程序无需以这种方式运行。

以下自适应镶嵌渲染状态及其默认值都是 DirectX 9.0 的新增内容：

D3DRS \_ MAXTESSELLATIONLEVEL = 1.0 f

D3DRS \_ MINTESSELLATIONLEVEL = 1.0 f

D3DRS \_ ADAPTIVETESS \_ X = 0.0 f

D3DRS \_ ADAPTIVETESS \_ Y = 0.0 f

D3DRS \_ ADAPTIVETESS \_ Z = 1.0 f

D3DRS \_ ADAPTIVETESS \_ W = 0.0 f

D3DRS \_ ENABLEADAPTIVETESSELLATION = **FALSE**

D3DDMAPSAMPLER 采样器也是 DirectX 9.0 的新示例，用于分割单元以设置置换地图纹理。

**注意**   DirectX 9.0 和更高版本的应用程序可使用 \_ D3DSAMPLERSTATETYPE 枚举中的 D3DSAMP DMAPOFFSET 值控制 presampled 置换地图中的偏移量（以顶点为）。 运行时将用户模式采样器状态映射 (D3DSAMP \_ *Xxx*) 为内核模式 D3DTSS \_ *Xxx* 值，以便不需要 DirectX 9.0 和更高版本的驱动程序来处理用户模式采样器状态。 因此，驱动程序必须改为处理 \_ DP2TEXTURESTAGESTATE D3DDP2OP 操作的 [**D3DHAL \_ TEXTURESTAGESTATE**](/windows-hardware/drivers/ddi/d3dhal/ns-d3dhal-_d3dhal_dp2texturestagestate)结构的 **TSState** 成员中的 D3DTSS DMAPOFFSET 值 \_ 。 有关 D3DSAMPLERSTATETYPE 和 presampled 置换映射的详细信息，请参阅最新的 DirectX SDK 文档。

 

 

