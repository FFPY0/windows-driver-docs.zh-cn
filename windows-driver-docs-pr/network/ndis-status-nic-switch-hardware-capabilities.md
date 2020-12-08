---
title: NDIS_STATUS_NIC_SWITCH_HARDWARE_CAPABILITIES
description: NDIS_STATUS_NIC_SWITCH_HARDWARE_CAPABILITIES 状态向 NDIS 和过量驱动程序指示网络适配器中 NIC 交换机的硬件功能已更改。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 NDIS_STATUS_NIC_SWITCH_HARDWARE_CAPABILITIES 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d06db6dd21ee8bdd0b4a8333e823697e19b25a59
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837185"
---
# <a name="ndis_status_nic_switch_hardware_capabilities"></a>NDIS \_ 状态 \_ NIC \_ 交换机 \_ 硬件 \_ 功能


**Ndis \_ 状态 \_ NIC \_ 交换机 \_ 硬件 \_ 功能** 向 ndis 和过量驱动程序指示网络适配器中 NIC 交换机的硬件功能已更改。 这些功能包括 INF 文件设置当前禁用的硬件功能，或通过 " **高级** 属性" 页禁用的硬件功能。

状态指示由网络适配器 PCI Express (PCIe 的微型端口驱动程序) 物理功能 (PF) 。 PF 微型端口驱动程序在 Hyper-v 父分区的管理操作系统中运行。

<a name="remarks"></a>备注
-------

每当检测到网络适配器上的 NIC 交换机的硬件功能发生变化时，PF 微型端口驱动程序必须发出 **NDIS \_ 状态 \_ NIC \_ 交换机 \_ 硬件 \_ 功能** 状态指示。 当满足以下条件之一时，这些功能可能会更改：

-   NIC 交换机硬件功能通过独立硬件供应商 (IHV) 开发的管理应用程序启用或禁用。

-   NIC 交换机硬件功能对于属于负载平衡故障转移 (LBFO) 由 MUX 中间驱动程序管理的团队的一个或多个网络适配器进行了更改。 有关详细信息，请参阅 [NDIS MUX 中间驱动程序](./ndis-mux-intermediate-drivers.md)。

当 PF 微型端口驱动程序发出 **NDIS \_ 状态 \_ NIC \_ 交换机 \_ 硬件 \_ 功能** 状态指示时，必须执行以下步骤：

1.  微型端口驱动程序使用网络适配器的 NIC 交换机的硬件功能初始化 [**NDIS \_ NIC \_ 交换机 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities) 结构。
2.  微型端口驱动程序通过以下方式初始化 [**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication) 结构：

    -   **StatusCode** 成员必须设置为 **NDIS \_ 状态 \_ NIC \_ 交换机 \_ 硬件 \_ 功能**。

    -   **StatusBuffer** 成员必须设置为指向 [**NDIS \_ NIC \_ 交换机 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)结构的指针。 此结构包含 NIC 交换机的硬件功能。

    -   **StatusBufferSize** 成员必须设置为 Sizeof ([**NDIS \_ NIC \_ 交换机 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)) 。

3.  PF 微型端口驱动程序通过调用 [**NdisMIndicateStatusEx**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismindicatestatusex)发出状态通知。 驱动程序必须将指向 [**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication) 结构的指针传递到 *StatusIndication* 参数。

过量驱动程序可以使用 **NDIS \_ 状态 \_ NIC \_ 交换机 \_ 硬件 \_ 功能** 状态指示来确定网络适配器上当前启用的 NIC 交换机功能。 此外，这些驱动程序还可以发出 oid [ \_ NIC \_ 交换机 \_ 硬件 \_ 功能](oid-nic-switch-hardware-capabilities.md) 的 oid 查询请求，以随时获取这些功能。

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
<td><p>在 NDIS 6.30 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ndis。h</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


****
[**NDIS \_ NIC \_ 交换机 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_nic_switch_capabilities)

[**NDIS \_ 状态 \_ 指示**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_status_indication)

[OID \_ NIC \_ 交换机 \_ 硬件 \_ 功能](oid-nic-switch-hardware-capabilities.md)

 

