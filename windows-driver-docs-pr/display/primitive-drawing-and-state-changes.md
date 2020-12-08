---
title: 基元绘制和状态更改
description: 基元绘制和状态更改
keywords:
- Direct3D WDK Windows 2000 显示，基元绘图
- Direct3D WDK Windows 2000 显示，状态更改
- 状态 WDK Direct3D
- 基元绘图 WDK Direct3D
- D3dDrawPrimitives2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7c456805bcf3d37701d86ec15d32c10c08ce5361
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840999"
---
# <a name="primitive-drawing-and-state-changes"></a>基元绘制和状态更改


## <span id="ddk_primitive_drawing_and_state_changes_gg"></span><span id="DDK_PRIMITIVE_DRAWING_AND_STATE_CHANGES_GG"></span>


所有 Microsoft Direct3D 图形基元和状态更改都将传递到命令和顶点缓冲区中的 [**D3dDrawPrimitives2**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb) 回调。 驱动程序必须分析这些缓冲区并处理所有绘图和状态更改请求。

以下部分介绍了命令和顶点缓冲区的布局，并说明了驱动程序应如何处理它们：

[命令和顶点缓冲区](command-and-vertex-buffers.md)

[Direct3D 命令缓冲区](direct3d-command-buffers.md)

[Direct3D 顶点缓冲区](direct3d-vertex-buffers.md)

[加速状态管理](accelerated-state-management.md)

 

