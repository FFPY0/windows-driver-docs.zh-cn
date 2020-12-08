---
title: 从 NIC 中删除安全关联
description: 从 NIC 中删除安全关联
keywords:
- 安全关联 WDK IPsec 卸载
- SAs WDK IPsec 卸载
- 受 ESP 保护的数据包 WDK IPsec 卸载，安全关联
- 受 AH 保护的数据包 WDK IPsec 卸载，安全关联
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 54549407fadd9304a8fa0bf9efa9fef813b84ae1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814951"
---
# <a name="deleting-a-security-association-from-a-nic"></a>从 NIC 中删除安全关联

\[IPsec 任务卸载功能已弃用，不应使用。\]




如有必要，TCP/IP 传输可以设置 [OID \_ TCP \_ 任务 \_ IPSEC \_ DELETE \_ SA](./oid-tcp-task-ipsec-delete-sa.md) 来请求微型端口驱动程序从 NIC 中删除 (SA) 的安全关联。

若要为 NIC 上的另一个 SA 创建空间，微型端口驱动程序可以在接收数据包的 [**NDIS \_ IPSEC \_ 卸载 \_ V1 \_ 网络 \_ 缓冲区 \_ 列表 \_ 信息**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_ipsec_offload_v1_net_buffer_list_info)结构中设置 **SaDeleteReq** 标志。 接下来，TCP/IP 传输会发出 OID \_ TCP \_ 任务 \_ IPSEC \_ delete \_ SA，以便删除接收数据包 (SA) 的入站安全关联，并在另一次删除与已删除的入站 sa 相对应的出站 sa。 NIC 在收到相应的 OID \_ TCP \_ 任务 \_ IPSEC \_ DELETE \_ SA 请求之前，不能删除其中的任何一种。 微型端口驱动程序可以独立于 **CryptoDone** 标志来设置 **SaDeleteReq** 。
