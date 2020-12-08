---
title: KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ ROLLOFFFACTOR
description: KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ ROLLOFFFACTOR 属性指定3d 侦听器的 rolloff 系数。
keywords:
- KSPROPERTY_DIRECTSOUND3DLISTENER_ROLLOFFFACTOR 音频设备
topic_type:
- apiref
api_name:
- KSPROPERTY_DIRECTSOUND3DLISTENER_ROLLOFFFACTOR
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: ff598f1571744a1ff9b420a9bb29b35aca7d763b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784373"
---
# <a name="ksproperty_directsound3dlistener_rollofffactor"></a>KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ ROLLOFFFACTOR


KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ ROLLOFFFACTOR 属性指定3d 侦听器的 rolloff 系数。

## <span id="ddk_ksproperty_directsound3dlistener_rollofffactor_ks"></span><span id="DDK_KSPROPERTY_DIRECTSOUND3DLISTENER_ROLLOFFFACTOR_KS"></span>


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
<td align="left"><p>Pin</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty" data-raw-source="[&lt;strong&gt;KSNODEPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksnodeproperty)"><strong>KSNODEPROPERTY</strong></a></p></td>
<td align="left"><p>FLOAT</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值为 FLOAT 类型，并指定 rolloff 系数。 Rolloff 因子的范围可以是从 DS3D \_ MINROLLOFFFACTOR 到 DS3D \_ MAXROLLOFFFACTOR，它们分别定义为0.0 和10.0。 默认的 rolloff 因素是 DS3D \_ DEFAULTROLLOFFFACTOR，它定义为1.0。

### <a name="span-idreturn_valuespanspan-idreturn_valuespanspan-idreturn_valuespanreturn-value"></a><span id="Return_Value"></span><span id="return_value"></span><span id="RETURN_VALUE"></span>返回值

KSPROPERTY \_ DIRECTSOUND3DLISTENER \_ ROLLOFFFACTOR 属性请求返回状态 \_ SUCCESS 以指示该请求已成功完成。 否则，请求将返回相应的错误状态代码。

<a name="remarks"></a>备注
-------

Rolloff 是根据侦听器与声音源之间的距离应用到声音的衰减量。 如果 rolloff 因子为零，则表示不会对声音应用衰减，而不管它与侦听器之间的距离。 大于1的系数夸大是声音与距离的实际衰减。

DirectSound 使用此属性实现 **IDirectSound3DListener：： GetRolloffFactor** 和 **IDirectSound3DListener：： SetRolloffFactor** 方法，如 Microsoft Windows SDK 文档中所述。

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

