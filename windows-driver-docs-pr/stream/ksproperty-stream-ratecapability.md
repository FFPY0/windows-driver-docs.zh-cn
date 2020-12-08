---
title: KSPROPERTY \_ 流 \_ RATECAPABILITY
description: 使用 KSPROPERTY \_ STREAM \_ RATECAPABILITY 属性，图形管理器可以查询特定流的流中涉及的所有连接点， (通过 KSPROPERTY PIN DATAROUTING) 获取该流， \_ \_ 以便在将请求速率调整为名义速率时获得相应的功能。
keywords:
- KSPROPERTY_STREAM_RATECAPABILITY 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_STREAM_RATECAPABILITY
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d131d4eb1667fa9901a731b06d74fb4499cbef64
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817043"
---
# <a name="ksproperty_stream_ratecapability"></a>KSPROPERTY \_ 流 \_ RATECAPABILITY


使用 KSPROPERTY \_ STREAM \_ RATECAPABILITY 属性，图形管理器可以查询特定流的流中涉及的所有连接点， (通过 KSPROPERTY PIN DATAROUTING) 获取该流， \_ \_ 以便在将请求速率调整为名义速率时获得相应的功能。

## <span id="ddk_ksproperty_stream_ratecapability_ks"></span><span id="DDK_KSPROPERTY_STREAM_RATECAPABILITY_KS"></span>


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
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksrate" data-raw-source="[&lt;strong&gt;KSRATE&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksrate)"><strong>KSRATE</strong></a></p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksrate_capability" data-raw-source="[&lt;strong&gt;KSRATE_CAPABILITY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksrate_capability)"><strong>KSRATE_CAPABILITY</strong></a></p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

\_ \_ 如果 pin 允许速率改变，或者界定闭合相关 pin 之间的接口不同并导致使用不同的时间戳格式，则应该实现 KSPROPERTY STREAM RATECAPABILITY。 属性还可用于转换一般时间戳格式，如跳过降级请求。

通过重新采样或时间戳更改修改数据速率的 pin 支持属性。 所有速率更改都涉及请求费率，并确定特定的 pin 可以纠正该速率以获得标称1.0 速率的程度。 例如，请求视频播放速率为2.0 的 pin 表示请求呈现为视频剪辑的标称速率的两倍;速率为0.5 的速率请求表示半速渲染。

Rate 请求包含表示开始时间和该速率请求的持续时间。 这允许使用可能适用于数据流特定部分的约束。 显示时间、分子/分母对和持续时间单位用结构中指定的接口表示。 如果未使用标准接口，则不能将初始速率更改查询发送到 pin。

Pin 必须能够接受具有类似拓扑的任何 pin 所使用的接口标识符。 它还必须将接口标识符和时间单位转换为其相应的值。 通过这种方式，客户端可以从一个已知的接口点遍历关系图，并在每个步骤中使用连接点来转换单元。

如果即使无法更改速率，则支持此属性是很重要的，因此，在进行查询时可以调整接口和时间单位。 结果不会更改返回的速率，但会更改 Interface、PresentationStart 和 Duration。

仅可在 "暂停" 或 "运行" 状态中执行速率功能请求，并在更改为任何其他状态后变为无效。 速度最初为1.0 的查询应始终成功，因为通常只是请求翻译时间戳格式。

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


[**KSRATE**](/windows-hardware/drivers/ddi/ks/ns-ks-ksrate)

[**KSRATE \_ 功能**](/windows-hardware/drivers/ddi/ks/ns-ks-ksrate_capability)

