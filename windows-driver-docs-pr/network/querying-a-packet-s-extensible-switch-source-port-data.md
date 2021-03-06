---
title: 查询数据包的可扩展交换机源端口数据
description: 查询数据包的可扩展交换机源端口数据
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 34adcdc9fbc35c4e5445dc749d2069da710c45c1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820045"
---
# <a name="querying-a-packets-extensible-switch-source-port-data"></a>查询数据包的可扩展交换机源端口数据


Hyper-v 可扩展交换机源端口由 [**NDIS \_ 交换机 \_ 转发 \_ 详细信息 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_detail_net_buffer_list_info)结构中的 **SourcePortId** 成员指定。 此结构包含在数据包的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_buffer_list) 结构的带外 (OOB) 转发上下文中。 有关此上下文的详细信息，请参阅 [Hyper-v 可扩展交换机转发上下文](hyper-v-extensible-switch-forwarding-context.md)。

可扩展交换机扩展使用 [**网络 \_ 缓冲区 \_ 列表 \_ 交换机 \_ 转发 \_ 详细**](/windows-hardware/drivers/ddi/ndis/nf-ndis-net_buffer_list_switch_forwarding_detail)信息宏访问 [**NDIS \_ 交换机 \_ 转发 \_ 详细信息 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_switch_forwarding_detail_net_buffer_list_info)结构。 以下示例演示了驱动程序如何从数据包的 **NDIS \_ 交换机 \_ 转发 \_ 详细信息 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息** 结构获取源端口标识符。

```C++
PNDIS_SWITCH_FORWARDING_DETAIL_NET_BUFFER_LIST_INFO fwdDetail;
NDIS_SWITCH_PORT_ID sourcePortId;

fwdDetail = NET_BUFFER_LIST_SWITCH_FORWARDING_DETAIL(NetBufferList);
sourcePortId = fwdDetail->SourcePortId;
```

 

