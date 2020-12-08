---
title: KSPROPERTY \_ 调谐器 \_ 模式
description: 用户模式客户端使用 KSPROPERTY \_ 调谐器 \_ 模式属性来获取或设置设备的优化模式，如模拟电视、数字电视、FM、AM 或 DSS。 必须实现此属性。
keywords:
- KSPROPERTY_TUNER_MODE 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_TUNER_MODE
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9eec89e7dc17974ad779c5b670b1cdf58e6c16bc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790175"
---
# <a name="ksproperty_tuner_mode"></a>KSPROPERTY \_ 调谐器 \_ 模式


用户模式客户端使用 KSPROPERTY \_ 调谐器 \_ 模式属性来获取或设置设备的优化模式，如模拟电视、数字电视、FM、AM 或 DSS。 必须实现此属性。

## <span id="ddk_ksproperty_tuner_mode_ks"></span><span id="DDK_KSPROPERTY_TUNER_MODE_KS"></span>


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
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_mode_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_MODE_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_mode_s)"><strong>KSPROPERTY_TUNER_MODE_S</strong></a></p></td>
<td><p>ULONG</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是一个 ULONG，用于指定调谐器的当前优化模式。

<a name="remarks"></a>备注
-------

KSPROPERTY **Mode** \_ 调谐器 \_ 模式 S 结构的 Mode 成员 \_ 指定当前调谐器模式。

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

[**KSPROPERTY \_ 调谐器 \_ 模式 \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_mode_s)

