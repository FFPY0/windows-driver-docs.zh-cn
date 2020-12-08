---
title: OID_GEN_PCI_DEVICE_CUSTOM_PROPERTIES
description: 作为查询，过量驱动程序使用 OID_GEN_PCI_DEVICE_CUSTOM_PROPERTIES OID 获取设备的 PCI 自定义属性。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_PCI_DEVICE_CUSTOM_PROPERTIES 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 185226a27c21a519ae2434539152c08c1de9d3de
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829457"
---
# <a name="oid_gen_pci_device_custom_properties"></a>OID \_ 生成 \_ PCI \_ 设备 \_ 自定义 \_ 属性


作为查询，过量驱动程序使用 OID 第一 \_ 代 \_ PCI \_ 设备 \_ 自定义 \_ 属性 OID 获取设备的 PCI 自定义属性。

<a name="remarks"></a>备注
-------

NDIS 处理 OID \_ 生成 \_ PCI \_ 设备 \_ 自定义 \_ 属性和微型端口驱动程序不会收到 oid 查询。

此查询对于其他 NDIS 驱动程序是可选的。

NDIS 返回了包含 PCI 自定义属性的 [**ndis \_ PCI \_ 设备 \_ 自定义 \_ 属性**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pci_device_custom_properties) 结构。

对于非 PCI 微型端口适配器，NDIS 无法 \_ \_ \_ \_ \_ 通过具有 NDIS \_ 状态 " \_ \_ 设备 \_ 请求状态代码无效" 的 OID 生成 PCI 设备自定义属性。

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
<td><p>在 NDIS 6.0 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS \_ PCI \_ 设备 \_ 自定义 \_ 属性**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pci_device_custom_properties)

 

