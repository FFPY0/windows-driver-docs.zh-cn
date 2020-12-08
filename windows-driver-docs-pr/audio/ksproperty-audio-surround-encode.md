---
title: KSPROPERTY \_ 音频 \_ 环绕 \_ 编码
description: "\"KSPROPERTY \\_ 音频 \\_ 环绕 \\_ 编码\" 属性指定是启用还是禁用筛选器的环绕编码器。 环绕编码器节点 (KSNODETYPE \\_ PROLOGIC \\_ 编码器) 执行杜能环绕 Pro 逻辑编码。"
keywords:
- KSPROPERTY_AUDIO_SURROUND_ENCODE 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_AUDIO_SURROUND_ENCODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4bc1fe494a0258bd53b56f374a697bf3802bd01c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798985"
---
# <a name="ksproperty_audio_surround_encode"></a>KSPROPERTY \_ 音频 \_ 环绕 \_ 编码


"KSPROPERTY \_ 音频 \_ 环绕 \_ 编码" 属性指定是启用还是禁用筛选器的环绕编码器。 环绕编码器节点 ([**KSNODETYPE \_ PROLOGIC \_ 编码器**](ksnodetype-prologic-encoder.md)) 执行杜能环绕 Pro 逻辑编码。

## <span id="ddk_ksproperty_audio_surround_encode_ks"></span><span id="DDK_KSPROPERTY_AUDIO_SURROUND_ENCODE_KS"></span>


### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="Usage_Summary_Table"></span><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用情况摘要表

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
<th align="left">获取</th>
<th align="left">设置</th>
<th align="left">目标</th>
<th align="left">属性描述符类型</th>
<th align="left">属性值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>是</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>筛选器</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>BOOL</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值为 BOOL 类型，指示是否启用了环绕编码器节点。 如果值为 **TRUE** ，则表示已启用环绕编码器节点。 **FALSE** 指示它处于禁用状态。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ 音频 \_ 环绕 \_ 编码属性请求返回状态 " \_ 成功" 以指示它已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

在 Microsoft Windows XP 和更高版本中， [KMixer 系统驱动程序](./kernel-mode-wdm-audio-components.md#kmixer-system-driver) 支持 KSPROPERTY \_ 音频 \_ 环绕 \_ 编码属性。

如果启用，则环绕编码器节点会将 "左"、"右"、"右" 和 "背面" 扬声器) 的通道编码为四通道输入 (流，并将其到环绕式的立体声输出流中。 例如，可以通过 [**KSNODETYPE \_ PROLOGIC \_ 解码器**](ksnodetype-prologic-decoder.md) 节点对此输出流进行解码。 它还可以通过音频设备的模拟立体声输出来播放，这些输出可连接到直接推动左、右、居中和背面扬声器的外部环绕解码器。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**KSNODEPROPERTY**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)

[**KSNODETYPE \_ PROLOGIC \_ 编码器**](ksnodetype-prologic-encoder.md)

[**KSNODETYPE \_ PROLOGIC \_ 解码器**](ksnodetype-prologic-decoder.md)

