---
title: KSPROPERTY \_ 调谐器 \_ 状态
description: KSPROPERTY \_ 调谐器 \_ STATUS 属性检索有关优化过程的信息，包括当前频率、相位锁定循环 (PLL) 偏移量和信号强度。 必须实现此属性。
keywords:
- KSPROPERTY_TUNER_STATUS 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_TUNER_STATUS
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67f27a78824325fccb3bcebbe002070e17a8bb3f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805969"
---
# <a name="ksproperty_tuner_status"></a>KSPROPERTY \_ 调谐器 \_ 状态


KSPROPERTY \_ 调谐器 \_ STATUS 属性检索有关优化过程的信息，包括当前频率、相位锁定循环 (PLL) 偏移量和信号强度。 必须实现此属性。

## <span id="ddk_ksproperty_tuner_status_ks"></span><span id="DDK_KSPROPERTY_TUNER_STATUS_KS"></span>


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
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_status_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_STATUS_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_status_s)"><strong>KSPROPERTY_TUNER_STATUS_S</strong></a></p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_status_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_TUNER_STATUS_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_status_s)"><strong>KSPROPERTY_TUNER_STATUS_S</strong></a></p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是一个 KSPROPERTY \_ 调谐器 \_ 状态 \_ S 结构，它指定当前频率、PLL 偏移量和信号强度。

<a name="remarks"></a>备注
-------

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

[**KSPROPERTY \_ 调谐器 \_ 状态 \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_tuner_status_s)

