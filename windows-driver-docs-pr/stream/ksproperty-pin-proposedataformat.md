---
title: KSPROPERTY \_ PIN \_ PROPOSEDATAFORMAT
description: 客户端使用 KSPROPERTY \_ 引脚 \_ PROPOSEDATAFORMAT 属性来确定 pin 工厂实例化的 pin 是否支持特定的数据格式。
keywords:
- KSPROPERTY_PIN_PROPOSEDATAFORMAT 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_PIN_PROPOSEDATAFORMAT
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 12/28/2018
ms.localizationpriority: medium
ms.openlocfilehash: 7a139233a0b4785b30cbd0573e77f60e6270f226
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811353"
---
# <a name="ksproperty_pin_proposedataformat"></a>KSPROPERTY \_ PIN \_ PROPOSEDATAFORMAT

客户端使用 KSPROPERTY \_ 引脚 \_ PROPOSEDATAFORMAT 属性来确定 pin 工厂实例化的 pin 是否支持特定的数据格式。

## <a name="usage-summary-table"></a>使用情况摘要表

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
<td><p>筛选器</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)"><strong>KSP_PIN</strong></a></p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat" data-raw-source="[&lt;strong&gt;KSDATAFORMAT&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)"><strong>KSDATAFORMAT</strong></a></p></td>
</tr>
</tbody>
</table>

## <a name="remarks"></a>备注

KSPROPERTY_PIN_PROPOSEDATAFORMAT 包括 KSDATAFORMAT 类型的结构，并指定建议的数据格式。 使用 KSP_PIN 指定此属性，其中成员指定相关的 PIN 工厂。

KSPROPERTY \_ PIN \_ PROPOSEDATAFORMAT 包含类型为 [**KSDATAFORMAT**](/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)的结构，该结构指定建议的数据格式。

[**KSPROPERTY \_Windows \_**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier) 7 和更高版本的 WINDOWS 支持类型 GET。 在 Windows Vista 中，*不支持* **KSPROPERTY \_ 类型 \_ GET** 。

使用此属性 **KSPROPERTY_TYPE_GET** 允许音频驱动程序提供有关 pin 的默认数据格式的信息。 **KSPROPERTY_TYPE_GET** 对于此属性是可选的，除非该驱动程序支持 [**KSEVENT_PINCAPS_FORMATCHANGE**](../audio/ksevent-pincaps-formatchange.md)。

\_如果可以将 pin 设置为或使用建议的数据格式打开，则在将此属性与 KSPROPERTY_TYPE_SET 一起使用时，KS 筛选器将返回状态成功。 如果无法将 pin 设置为建议的数据格式，则它将返回 STATUS_NO_MATCH。 对于其他任何失败，将返回相应的错误。 如果驱动程序支持 [**KSPROPERTY_AUDIOSIGNALPROCESSING_MODES**](../audio/ksproperty-audiosignalprocessing-modes.md)，则此属性应返回 STATUS_SUCCESS 如果任何音频信号处理模式支持该格式。

使用带有此属性的 KSPROPERTY_TYPE_SET 实际上不会更改数据格式。 客户端使用 [**KSPROPERTY \_ 连接 \_ DATAFORMAT**](ksproperty-connection-dataformat.md) 来更改数据格式。 对于此属性， **KSPROPERTY_TYPE_SET** 是可选的。

## <a name="requirements"></a>要求

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

[**KSP \_ PIN**](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)

[**KSDATAFORMAT**](/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat)

[**KSEVENT_PINCAPS_FORMATCHANGE**](../audio/ksevent-pincaps-formatchange.md)

[**KS 属性**](./ks-properties.md)

[**KSPROPERTY \_ 类型 \_ GET**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSPROPERTY_AUDIOSIGNALPROCESSING_MODES**](../audio/ksproperty-audiosignalprocessing-modes.md)
