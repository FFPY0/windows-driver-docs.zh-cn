---
title: KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ PHOTOTRIGGERTIME
description: 此属性控制照相机驱动程序的触发时间。 触发时间用于确定照片序列的参考框架。
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOTRIGGERTIME 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_PHOTOTRIGGERTIME
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 18395b9dab5858807004417517174eb7f59e6e47
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837855"
---
# <a name="ksproperty_cameracontrol_extended_phototriggertime"></a>KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ PHOTOTRIGGERTIME

此属性控制照相机驱动程序的触发时间。 触发时间用于确定照片序列的参考框架。

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
<td><p>Pin</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_HEADER&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)"><strong>KSCAMERA_EXTENDEDPROP_HEADER</strong></a></p></td>
</tr>
</tbody>
</table>

属性值 (操作数据) 包含 [**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header) 结构和 [**KSCAMERA \_ EXTENDEDPROP \_ 值**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value) 结构。 以100毫微秒为单位的照片触发时间设置或返回为 **KSCAMERA \_ EXTENDEDPROP \_ 值** 中的值。

总的属性数据大小为 **sizeof** (KSCAMERA \_ EXTENDEDPROP \_ 标头) + **sizeof** (KSCAMERA \_ EXTENDEDPROP \_ VALUE) 。 [**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的 **Size** 成员设置为此总属性数据大小。

使用 [**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的 **flags** 成员中的下列标志之一设置或清除触发器时间。

| 触发时间标志                           | 描述                     |
|---------------------------------------------|---------------------------------|
| KSPROPERTY \_ 摄影机 \_ PHOTOTRIGGERTIME \_ CLEAR | 清除 "触发器时间" 设置。 |
| KSPROPERTY \_ 照相机 \_ PHOTOTRIGGERTIME \_ 集   | 设置新的触发器时间值。   |

此属性控件是同步的，并且不可取消。

## <a name="remarks"></a>备注

### <a name="getting-the-property"></a>获取属性

当响应 KSPROPERTY \_ 类型 \_ GET 请求时，驱动程序会将 [**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header) 的成员设置为以下项。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>成员</th>
<th>“值”</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>版本</td>
<td>1</td>
</tr>
<tr class="even">
<td>PinId</td>
<td>照片 pin 的 pin ID。</td>
</tr>
<tr class="odd">
<td>大小</td>
<td><p>sizeof (KSCAMERA_EXTENDEDPROP_HEADER) +</p>
<p>sizeof (KSCAMERA_EXTENDEDPROP_VALUE) </p></td>
</tr>
<tr class="even">
<td>结果</td>
<td><p>尝试读取最大帧速率导致的错误值。</p>
<p>否则为 0。</p></td>
</tr>
<tr class="odd">
<td>功能</td>
<td>0</td>
</tr>
<tr class="even">
<td>Flags</td>
<td>设置或清除标志</td>
</tr>
</tbody>
</table>

如果触发器时间当前未设置为任何时间值，则 [**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header)的 **Flags** 成员必须包含 KSPROPERTY \_ 摄像 \_ PHOTOTRIGGERTIME \_ CLEAR 值。

### <a name="setting-the-property"></a>设置属性

设置属性时， [**KSCAMERA \_ EXTENDEDPROP \_ 值**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_value)的 **u)** 成员将包含触发器时间值。 触发器时间基于操作标志进行设置或清除。 当标志为 KSPROPERTY \_ 摄像 PHOTOTRIGGERTIME 时， \_ \_ 不使用 **KSCAMERA \_ EXTENDEDPROP \_ 值** 中的值，将忽略该值。

## <a name="requirements"></a>要求

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>可从 Windows 8.1 开始。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>
