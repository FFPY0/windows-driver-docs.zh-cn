---
title: 纹理位图传送
description: 纹理位图传送
keywords:
- blt WDK Direct3D
- 纹理管理 WDK Direct3D，blitting
- blitting WDK Direct3D
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 753c5534a2d69a47b38c0096fea58d854f843bdb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839567"
---
# <a name="texture-blitting"></a>纹理位图传送


## <span id="ddk_texture_blitting_gg"></span><span id="DDK_TEXTURE_BLITTING_GG"></span>


在 DirectX 7.0 中引入的 Direct3D DDI 的一项重要变化是，通过在 [**D3dDrawPrimitives2**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_drawprimitives2cb) 命令流中嵌入令牌来 blitted 纹理。 此令牌是 D3DDP2OP \_ TEXBLT，它指示驱动程序必须将纹理从后备表面传输到本地或非本地视频内存。

此外，运行时还会将句柄号分配给在 Direct3D 上下文中创建 *D3dTextureCreate* 的每 *D3dTextureDestroy* 个 DirectDrawSurface 对象，而不是负责创建纹理的内部句柄。 该驱动程序通过 [**D3dCreateSurfaceEx**](/windows/win32/api/ddrawint/nc-ddrawint-pdd_createsurfaceex) 回调发送此句柄编号的信号。

*D3dCreateSurfaceEx*) [*DdCreateSurface*](/previous-versions/windows/hardware/drivers/ff549263(v=vs.85)) 调用完成后，调用每个硬件抽象 (层后，将调用。 *D3dCreateSurfaceEx*) **CreateSurface** 调用完成后，还会在每个内部硬件仿真层 (HEL 调用。 创建后备 DirectDrawSurface 对象时通常会发生 HEL 调用。 这些调用可能会在使用 [**D3dContextCreate**](/windows-hardware/drivers/ddi/d3dhal/nc-d3dhal-lpd3dhal_contextcreatecb)创建 Direct3D 上下文之前和之后发生。

此外，在应用程序运行时，对 [**D3dDestroyDDLocal**](/windows/win32/api/ddrawint/nc-ddrawint-pdd_destroyddlocal) 进行调用，以清理并销毁为这些图面显式创建的任何驱动程序数据。 此调用也在创建 Direct3D 上下文之前进行。 这样做是为了确保没有与未清理的任何上下文关联的脏句柄。 这只是一种预防措施，在使用后正确清理上下文时，不应实际销毁任何内容。

 

