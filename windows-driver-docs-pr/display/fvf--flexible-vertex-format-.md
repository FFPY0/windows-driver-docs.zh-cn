---
title: FVF（灵活顶点格式）
description: FVF（灵活顶点格式）
keywords:
- 顶点格式 WDK Direct3D
- 灵活顶点格式 WDK Direct3D
- FVF WDK Direct3D
- Direct3D WDK Windows 2000 显示，灵活顶点格式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b8ea54e9b99f37177a86592b0fa1678dcf3f128e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840763"
---
# <a name="fvf-flexible-vertex-format"></a>FVF（灵活顶点格式）


## <span id="ddk_fvf_gg"></span><span id="DDK_FVF_GG"></span>


驱动程序的 [**D3dDrawPrimitives2**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb) 回调以灵活的顶点格式 (FVF) 接收顶点数据。 由于顶点格式非常灵活，因此没有为此数据定义全面的数据结构。 驱动程序必须实现完全 FVF 的功能。

除了一般的2D 纹理以外，还提供了一项适用于 Microsoft DirectX 7.0 的 FVF 更新。 有关此更新的详细信息，请参阅 [FVF update](fvf-update.md)。 有关这些主题的详细信息，请参阅 *Perm3* 示例驱动程序和 DirectX SDK 文档。

**注意**   Microsoft Windows 驱动程序工具包 (WDK) 不包含 *Perm3*)  (的 3Dlabs Permedia3 示例显示驱动程序。 你可以从 Windows Server 2003 SP1 驱动程序开发工具包获取此示例驱动程序 (DDK) ，你可以从 WDHC 网站的 "Windows 驱动程序开发工具包" 页下载该驱动程序。

 

 

