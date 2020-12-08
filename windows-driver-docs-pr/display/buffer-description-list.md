---
title: 缓冲区说明列表
description: 缓冲区说明列表
keywords:
- 视频解码 WDK DirectX VA，缓冲区描述列表
- 解码视频 WDK DirectX VA，缓冲区描述列表
- 图片解码 WDK DirectX VA，缓冲区描述列表
- 缓冲 WDK DirectX VA
- 缓冲区描述列表 WDK DirectX VA
- DXVA_BufferDescription
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6ecf1973ce2c10615aa1b8c4b96108ad778c045f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810419"
---
# <a name="buffer-description-list"></a>缓冲区说明列表


## <span id="ddk_buffer_description_list_gg"></span><span id="DDK_BUFFER_DESCRIPTION_LIST_GG"></span>


DirectX VA 主要通过将数据缓冲区从主机解码器传递到硬件加速器来运行。 如果将一组缓冲区从主机传递到加速器，则会发送一个缓冲区说明列表来描述缓冲区。 缓冲区描述列表是 [**DXVA \_ BufferDescription**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_bufferdescription) 结构的数组。 "缓冲区说明" 列表包含一 \_ 组要发送的缓冲区中的每个缓冲区的 DXVA BufferDescription 结构。 缓冲区说明列表以一个或多个 DXVA \_ BufferDescription 结构开始，适用于所发送的第一种缓冲区。 后跟一个或多个 DXVA \_ BufferDescription 结构用于发送的下一个缓冲区，依此类推。

[**DXVA \_ BufferDescription**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_bufferdescription)结构的 **dwTypeIndex** 成员的值指定将哪种类型的缓冲区从主机传递到快捷键。

 

