---
title: SRB \_ 读取 \_ 数据
description: SRB \_ 读取 \_ 数据
keywords:
- SRB_READ_DATA 流媒体设备
topic_type:
- apiref
api_name:
- SRB_READ_DATA
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2e77aad8db26932afdd154440d9f94140c45910
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821751"
---
# <a name="srb_read_data"></a>SRB \_ 读取 \_ 数据


## <span id="ddk_srb_read_data_ks"></span><span id="DDK_SRB_READ_DATA_KS"></span>


类驱动程序已收到微型驱动程序的读取请求。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

微型驱动程序可以将以下项之一设置为 SRB 中的状态，也可以通过其他错误代码来指示错误情况，如内存错误和错误的参数。 类驱动程序仅检查状态 " \_ 成功"。

<span id="STATUS_SUCCESS"></span><span id="status_success"></span>状态 \_ 成功  
指示命令成功完成。

<span id="STATUS_NOT_IMPLEMENTED"></span><span id="status_not_implemented"></span>状态 \_ 未 \_ 实现  
指示微型驱动程序不支持该函数。

<span id="STATUS_IO_DEVICE_ERROR"></span><span id="status_io_device_error"></span>状态 \_ IO \_ 设备 \_ 错误  
指示出现硬件故障。

### <a name="comments"></a>注释

*PSrb* - &gt; **CommandData** 的值。**DataBufferArray** 指向 [**KSSTREAM \_ 标头**](/windows-hardware/drivers/ddi/ks/ns-ks-ksstream_header)结构的数组，它们共同描述了数据缓冲区。 *PSrb* 指针指向 [**HW \_ 流 \_ 请求 \_ 块**](/windows-hardware/drivers/ddi/strmini/ns-strmini-_hw_stream_request_block)结构。 *pSrb* - pSrb &gt;**CommandData**。**NumberOfBuffers** 指定数组的大小。

**当 \_ 微型驱动程序接收到 SRB READ \_ DATA 命令时，响应的微型驱动程序例程应：**

1.  检查以确定当前流状态。 在处于 "暂停" 或 "运行" 状态时，微型驱动程序只接受读取请求。 如果流已停止，则它应立即完成并返回 SRB。

2.  将 SRB 放在队列中。

 

