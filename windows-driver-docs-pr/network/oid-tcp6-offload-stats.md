---
title: OID_TCP6_OFFLOAD_STATS
description: 本主题介绍) OID_TCP6_OFFLOAD_STATS 对象标识符 (OID。
keywords:
- OID_TCP6_OFFLOAD_STATS
ms.date: 11/06/2017
ms.localizationpriority: medium
ms.openlocfilehash: c0addde94d2ea775f80bd3365b7f56362a759511
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832145"
---
# <a name="oid_tcp6_offload_stats"></a>OID_TCP6_OFFLOAD_STATS

宿主堆栈会查询 OID_TCP6_OFFLOAD_STATS OID，以获取在传递 IPv6 数据报的已卸载的 TCP 连接上对卸载目标处理的 TCP 段上的统计信息。 宿主堆栈设置此 OID，导致卸载目标将此类统计信息的计数器重置为零。

为了响应 OID_TCP6_OFFLOAD_STATS 的查询，卸载目标提供了一个已填充的 [TCP_OFFLOAD_STATS](/windows-hardware/drivers/ddi/ndischimney/ns-ndischimney-_tcp_offload_stats) 结构。

为了响应一组 OID_TCP6_OFFLOAD_STATS，卸载目标应重置为所有用于传递 IPv6 数据报的已卸载 TCP 连接的 TCP 统计信息计数器。

## <a name="requirements"></a>要求

**版本**： Windows Vista 和更高版本的 **标头**： Ntddndis (包括 Ndis .h) 
