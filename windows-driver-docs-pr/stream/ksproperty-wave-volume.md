---
title: KSPROPERTY \_ 波形 \_ 音量
description: KSPROPERTY \_ wave \_ volume 属性指定波形设备的音量设置。
keywords:
- KSPROPERTY_WAVE_VOLUME 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_WAVE_VOLUME
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: af4486d9e9087ea94a5b910647be7f7c48ee9cf6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801225"
---
# <a name="ksproperty_wave_volume"></a>KSPROPERTY \_ 波形 \_ 音量


KSPROPERTY \_ wave \_ volume 属性指定波形设备的音量设置。

## <span id="ddk_ksproperty_wave_volume_ks"></span><span id="DDK_KSPROPERTY_WAVE_VOLUME_KS"></span>


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
<td><p>是</p></td>
<td><p>Pin</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kswave_volume" data-raw-source="[&lt;strong&gt;KSWAVE_VOLUME&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kswave_volume)"><strong>KSWAVE_VOLUME</strong></a></p></td>
</tr>
</tbody>
</table>

 

) 操作数据 (的属性值是 KSWAVE 的 \_ 卷结构，用于描述左侧和右侧的衰减量。

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

[**KSWAVE \_ 卷**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-kswave_volume)

