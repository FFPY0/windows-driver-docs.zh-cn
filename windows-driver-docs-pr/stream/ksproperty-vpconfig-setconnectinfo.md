---
title: KSPROPERTY \_ VPCONFIG \_ SETCONNECTINFO
description: KSPROPERTY \_ VPCONFIG \_ SETCONNECTINFO 属性设置视频端口配置和用户定义的连接信息。 它是指向 KSPROPERTY \_ VPCONFIG GETCONNECTINFO 属性返回的 DDVIDEOPORTCONNECT 结构的数组的指针 \_ 。
keywords:
- KSPROPERTY_VPCONFIG_SETCONNECTINFO 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_VPCONFIG_SETCONNECTINFO
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 29423e429e30b33e583663d72ec3defeb8d8b9cb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811351"
---
# <a name="ksproperty_vpconfig_setconnectinfo"></a>KSPROPERTY \_ VPCONFIG \_ SETCONNECTINFO


KSPROPERTY \_ VPCONFIG \_ SETCONNECTINFO 属性设置视频端口配置和用户定义的连接信息。 它是指向 KSPROPERTY [**DDVIDEOPORTCONNECT**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddvideoportconnect) \_ VPCONFIG GETCONNECTINFO 属性返回的 DDVIDEOPORTCONNECT 结构的数组的指针 \_ 。

## <span id="ddk_ksproperty_vpconfig_setconnectinfo_ks"></span><span id="DDK_KSPROPERTY_VPCONFIG_SETCONNECTINFO_KS"></span>


### <a name="usage-summary-table"></a>使用情况摘要表

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>获取</th>
<th>设置</th>
<th>目标</th>
<th>属性描述符类型</th>
<th>属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>Pin</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddvideoportconnect" data-raw-source="[&lt;strong&gt;DDVIDEOPORTCONNECT&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddvideoportconnect)"><strong>DDVIDEOPORTCONNECT</strong></a></p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是描述视频端口连接配置的 DDVIDEOPORTCONNECT 结构。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**DDVIDEOPORTCONNECT**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddvideoportconnect)

[**KSPROPERTY \_ VPCONFIG \_ GETCONNECTINFO**](ksproperty-vpconfig-getconnectinfo.md)

