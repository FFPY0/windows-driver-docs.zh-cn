---
title: KSPROPERTY \_ 时钟 \_ PHYSICALTIME
description: 客户端使用 KSPROPERTY \_ 时钟的 " \_ 物理 \_ 时间" 属性来确定时钟的当前物理时间。
keywords:
- KSPROPERTY_CLOCK_PHYSICALTIME 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CLOCK_PHYSICALTIME
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b4fc446d28cff6427d56ef90f2e68fe67cfcfca
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789555"
---
# <a name="ksproperty_clock_physicaltime"></a>KSPROPERTY \_ 时钟 \_ PHYSICALTIME


客户端使用 KSPROPERTY \_ 时钟的 " \_ 物理 \_ 时间" 属性来确定时钟的当前物理时间。

## <span id="ddk_ksproperty_clock_physicaltime_ks"></span><span id="DDK_KSPROPERTY_CLOCK_PHYSICALTIME_KS"></span>


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
<td><p>是</p></td>
<td><p>否</p></td>
<td><p>Pin</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p>LONGLONG</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

此属性返回类型为 LONGLONG 的值，它表示以100毫微秒为单位的当前物理时间。

时钟的物理时间是一直前进的计数器。 与显示时间不同，它无法反转。

不需要使用时钟来支持100毫微秒的分辨率。 若要确定时钟分辨率，客户端可以使用 [**KSPROPERTY \_ 时钟 \_ 解析**](ksproperty-clock-resolution.md) 请求。

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
<td>Ks (包含 Ks .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPROPERTY \_ 时钟 \_ CORRELATEDPHYSICALTIME**](ksproperty-clock-correlatedphysicaltime.md)

[**KSPROPERTY \_ 时钟 \_ CORRELATEDTIME**](ksproperty-clock-correlatedtime.md)

