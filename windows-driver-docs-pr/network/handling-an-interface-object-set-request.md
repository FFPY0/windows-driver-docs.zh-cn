---
title: 处理接口对象设置请求
description: 处理接口对象设置请求
keywords:
- NDIS 网络接口 WDK，设置请求
- 网络接口 WDK，设置请求
- Oid WDK 网络，网络接口
- OID 请求 WDK 网络
- 设置请求 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3d504e98536ac7a96d010113e4f59320acae270
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788355"
---
# <a name="handling-an-interface-object-set-request"></a>处理接口对象设置请求


为了设置与 interface 对象相关联的数据，NDIS 调用接口提供程序的 [**ProviderSetObject**](/windows-hardware/drivers/ddi/ndis/nc-ndis-if_set_object) 函数。 \_ \_ 如果成功更改了数据或 ndis \_ 状态 \_ *Xxx* 错误代码，则此函数将返回 ndis 状态成功。

有关接口提供程序特定 OID 请求的列表，请参阅 [NDIS 网络接口 oid](./ndis-network-interface-oids.md)。 有关 NDIS 用于提供程序、微型端口适配器和筛选器模块以支持网络接口对象的 Oid 列表，请参阅 [用于 OID 映射的 Ndis 网络接口](mapping-of-ndis-network-interfaces-to-ndis-oids.md)。

[**ProviderSetObject**](/windows-hardware/drivers/ddi/ndis/nc-ndis-if_set_object)的 *ProviderIfContext* 参数处的句柄标识接口提供程序在调用 [**NdisIfRegisterInterface**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisifregisterinterface)函数以注册接口时传递到 NDIS 的上下文区域。 *ObjectId* 参数为正在设置的对象指定 OID。 *InputBufferLength* 和 *pInputBuffer* 参数分别提供输入缓冲区的长度和指向输入缓冲区的指针。

 

