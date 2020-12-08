---
title: KSPROPERTY \_ 波形 \_ 输出 \_ 功能
description: KSPROPERTY \_ wave \_ output \_ 功能属性返回波形设备的波形输出功能。
keywords:
- KSPROPERTY_WAVE_OUTPUT_CAPABILITIES 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_WAVE_OUTPUT_CAPABILITIES
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: db82b348f455e4f3db812a7877a68e8c2dc9026e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794163"
---
# <a name="ksproperty_wave_output_capabilities"></a>KSPROPERTY \_ 波形 \_ 输出 \_ 功能


KSPROPERTY \_ wave \_ output \_ 功能属性返回波形设备的波形输出功能。

## <span id="ddk_ksproperty_wave_output_capabilities_ks"></span><span id="DDK_KSPROPERTY_WAVE_OUTPUT_CAPABILITIES_KS"></span>


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
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kswave_output_capabilities" data-raw-source="[&lt;strong&gt;KSWAVE_OUTPUT_CAPABILITIES&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kswave_output_capabilities)"><strong>KSWAVE_OUTPUT_CAPABILITIES</strong></a></p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是一个 KSWAVE \_ 输出 \_ 功能结构，该结构描述了波形设备的输出功能，其中包括音频通道的最大数量、每个采样的位数、采样频率范围、总数和活动连接数。

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


[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSWAVE \_ 输出 \_ 功能**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kswave_output_capabilities)

