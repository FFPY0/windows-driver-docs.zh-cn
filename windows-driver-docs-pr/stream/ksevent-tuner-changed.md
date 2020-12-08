---
title: KSEVENT \_ 调谐器 \_ 已更改
description: KSEVENT \_ 调谐器 \_ CHANGED 事件会在用户模式下传播从内核模式视频捕获微型驱动程序到 DirectShow 的操作，例如通道更改。
keywords:
- KSEVENT_TUNER_CHANGED 流媒体设备
topic_type:
- apiref
api_name:
- KSEVENT_TUNER_CHANGED
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2601e22dbec67f5c445ab6caf195f7c4a7e93b60
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805973"
---
# <a name="ksevent_tuner_changed"></a>KSEVENT \_ 调谐器 \_ 已更改


KSEVENT \_ 调谐器 \_ CHANGED 事件会在用户模式下传播从内核模式视频捕获微型驱动程序到 DirectShow 的操作，例如通道更改。

## <span id="ddk_ksevent_tuner_changed_ks"></span><span id="DDK_KSEVENT_TUNER_CHANGED_KS"></span>


### <a name="span-idusage_summary_tablespanspan-idusage_summary_tablespanusage-summary-table"></a><span id="usage_summary_table"></span><span id="USAGE_SUMMARY_TABLE"></span>使用情况摘要表

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
<th>事件描述符类型</th>
<th>事件值类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>Pin</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-kse_node" data-raw-source="[&lt;strong&gt;KSE_NODE&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-kse_node)"><strong>KSE_NODE</strong></a></p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata" data-raw-source="[&lt;strong&gt;KSEVENTDATA&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-kseventdata)"><strong>KSEVENTDATA</strong></a></p></td>
</tr>
</tbody>
</table>

 

有关 DirectShow 筛选器和 KsProxy 的详细信息，请参阅 [内核流式处理代理](/windows-hardware/drivers/ddi/_stream/index)。

