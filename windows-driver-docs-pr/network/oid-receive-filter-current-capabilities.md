---
title: OID_RECEIVE_FILTER_CURRENT_CAPABILITIES
description: 过量驱动程序发出 OID_RECEIVE_FILTER_CURRENT_CAPABILITIES 的 OID 查询请求，以获取当前启用的网络适配器接收筛选功能。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_RECEIVE_FILTER_CURRENT_CAPABILITIES 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 2dca08913b11b88ba9ce54eefbaf668b2e298e1b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786101"
---
# <a name="oid_receive_filter_current_capabilities"></a>OID \_ 接收 \_ 筛选器 \_ 当前 \_ 功能


过量驱动程序发出 oid 查询请求，OID \_ 接收 \_ 筛选器 \_ 当前 \_ 功能，用于获取网络适配器的当前启用的接收筛选功能。

成功从 OID 查询请求返回后， [**ndis \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)结构的 **InformationBuffer** 成员包含指向 [**ndis \_ 接收 \_ 筛选器 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构的指针。

<a name="remarks"></a>备注
-------

NDIS 接收筛选器在以下 NDIS 接口中使用：

-   [NDIS 数据包合并](./ndis-packet-coalescing.md)。 有关如何在此接口中使用接收筛选器的详细信息，请参阅 [管理包合并接收筛选器](./guidelines-for-managing-packet-coalescing-receive-filters.md)。

-   [单个根 I/o 虚拟化 (sr-iov) ](./single-root-i-o-virtualization--sr-iov-.md)。 有关如何在此接口中使用接收筛选器的详细信息，请参阅 [设置虚拟端口上的接收筛选器](./setting-a-receive-filter-on-a-virtual-port.md)。

-   [虚拟机队列 (VMQ)](./virtual-machine-queue--vmq--in-ndis-6-20.md)。 有关如何在此接口中使用接收筛选器的详细信息，请参阅 [设置和清除 VMQ 筛选器](./setting-and-clearing-vmq-filters.md)。

从 NDIS 6.20 开始，微型端口驱动程序会在调用 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数时注册网络适配器的当前启用的接收筛选硬件功能。 微型端口驱动程序通过执行以下步骤来注册这些功能：

1.  驱动程序使用当前启用的接收筛选硬件功能初始化 [**NDIS \_ 接收 \_ 筛选器 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities) 结构。

2.  驱动程序初始化 [**ndis \_ 微型端口 \_ 适配器 \_ 硬件 \_ 辅助 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes) 结构，并将 **CurrentReceiveFilterCapabilities** 成员设置为指向 [**NDIS \_ 接收 \_ 筛选器 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities) 结构的指针。

3.  微型端口驱动程序调用 [**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes) 函数，并将 *MiniportAttributes* 参数设置为指向 [**NDIS \_ 微型端口 \_ 适配器 \_ 硬件 \_ 协助 \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes) 结构的指针。

过量协议和筛选器驱动程序不必发出 OID \_ 接收 \_ 筛选器 \_ 当前功能的 oid 查询请求 \_ 。 NDIS 按以下方式向这些驱动程序提供当前启用的接收筛选功能：

-   NDIS 在绑定操作过程中，将基础网络适配器的当前启用的接收筛选功能提供给 [**NDIS \_ 绑定 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)结构的 **ReceiveFilterCapabilities** 成员中的过量协议驱动程序。

-   NDIS 提供当前启用的接收筛选功能，以便在附加操作期间 [**ndis \_ 筛选器 \_ 附加 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_filter_attach_parameters)结构的 **ReceiveFilterCapabilities** 成员中的现有筛选器驱动程序。

### <a name="return-status-codes"></a>返回状态代码

NDIS 处理对 \_ \_ 微型端口驱动程序的 oid 接收筛选器当前功能的 oid 查询请求 \_ \_ ，并返回以下状态代码之一：

<a href="" id="ndis-status-success"></a>NDIS \_ 状态 \_ 成功  
请求已成功完成。 **InformationBuffer** 指向 [**NDIS \_ 接收 \_ 筛选器 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构。

<a href="" id="ndis-status-pending"></a>NDIS \_ 状态 \_ 挂起  
请求正在等待完成。 请求完成后，NDIS 会将最终状态代码和结果传递给调用方的 OID 请求完成处理程序。

<a href="" id="ndis-status-invalid-length"></a>NDIS \_ 状态 \_ 无效 \_ 长度  
信息缓冲区太短。 NDIS 设置 **数据。查询 \_ 信息。** 将 [**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request) 结构中的成员 BytesNeeded 为所需的最小缓冲区大小。

<a href="" id="ndis-status-not-supported"></a>\_ \_ 不支持 NDIS \_ 状态  
网络适配器不支持接收筛选。

<a href="" id="ndis-status-failure"></a>NDIS \_ 状态 \_ 故障  
由于其他原因，请求失败。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>在 NDIS 6.20 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS \_ 绑定 \_ 参数**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_bind_parameters)

[**NDIS \_ 微型端口 \_ 适配器 \_ 硬件 \_ 辅助 \_ 特性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_hardware_assist_attributes)

[**NDIS \_ OID \_ 请求**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_oid_request)

[**NDIS \_ 接收 \_ 筛选器 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)

