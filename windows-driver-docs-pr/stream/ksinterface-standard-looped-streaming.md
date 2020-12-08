---
title: KSINTERFACE \_ 标准 \_ 循环 \_ 流式处理
description: KSINTERFACE \_ 标准 \_ 循环 \_ 流式处理
keywords:
- KSINTERFACE_STANDARD_LOOPED_STREAMING 流媒体设备
topic_type:
- apiref
api_name:
- KSINTERFACE_STANDARD_LOOPED_STREAMING
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8ed7b01ed1a0bc25c352cf3f3b769b1831ea6b4f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790217"
---
# <a name="ksinterface_standard_looped_streaming"></a>KSINTERFACE \_ 标准 \_ 循环 \_ 流式处理


## <span id="ddk_ksinterface_standard_looped_streaming_ks"></span><span id="DDK_KSINTERFACE_STANDARD_LOOPED_STREAMING_KS"></span>


KSINTERFACE \_ 标准 \_ 循环 \_ 流接口由 DSound 的客户端使用。 在 Windows XP 发布时，Kmixer 和 Portcls 是唯一支持此接口的 KS 音频筛选器。

如果 pin 支持 KSINTERFACE \_ 标准 \_ 循环 \_ 流式处理，则相关筛选器将不会完成缓冲区，直到将 pin 置于 *停止* 状态。 筛选器通过连续循环遍历提交给筛选器的单个缓冲区中的数据来处理数据。

### <a name="see-also"></a>另请参阅

[KSINTERFACESETID \_Standard](ksinterfacesetid-standard.md)、 [**KSPIN \_ INTERFACE**](/previous-versions/ff563537(v=vs.85))、 [**KSPIN \_ 描述符**](/windows-hardware/drivers/ddi/ks/ns-ks-kspin_descriptor)

 

