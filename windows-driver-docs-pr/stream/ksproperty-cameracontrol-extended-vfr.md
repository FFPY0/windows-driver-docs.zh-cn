---
title: KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ VFR
description: KSPROPERTY \_ CAMERACONTROL \_ EXTENDED \_ VFR 是一个属性 ID，用于指定是否需要在驱动程序上使用可变的帧速率。
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_VFR 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_VFR
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 3d31b7fcfad48d9281e292f9beaa710e5541d9aa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820449"
---
# <a name="ksproperty_cameracontrol_extended_vfr"></a>KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ VFR

KSPROPERTY \_ CAMERACONTROL \_ EXTENDED \_ VFR 是一个属性 ID，用于指定是否需要在驱动程序上使用可变的帧速率。 这是仅用于视频 pin 的 pin 级别控制。 对于预览和照片，帧速率可变性完全取决于驱动程序，并且不能由客户端控制。

## <a name="usage-summary-table"></a>使用情况摘要表

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>范围</th>
<th>控制</th>
<th>类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>版本 1</p></td>
<td><p>Pin</p></td>
<td><p>Synchronous</p></td>
</tr>
</tbody>
</table>

以下标志可以放置在 **KSCAMERA \_ EXTENDEDPROP \_ 标头中。Flags** 字段，用于打开和关闭视频的可变帧速率。 默认值为 "驱动程序"。

```cpp
#define KSCAMERA_EXTENDEDPROP_VFR_OFF   0x0000000000000000  
#define KSCAMERA_EXTENDEDPROP_VFR_ON    0x0000000000000001
```
如果设置为 VFR \_ ，则驱动程序应提供视频 pin 的固定帧速率。

如果设置为 VFR \_ ，则驱动程序将自动确定帧速率，并根据视频 pin 的捕获条件和方案而有所不同。 如果 \_ 设置了 VFR ON，则所允许的最大帧速率将由嵌入到视频录制的媒体类型中嵌入的固定帧速率进一步决定。

如果驱动程序不支持视频的可变帧速率，则驱动程序不应实现此控制，并且将暗示可变的帧速率。

对于不支持动态切换 VFR 设置的驱动程序，此控件在视频录制过程中不起作用。 在这种情况下，驱动程序应忽略在活动视频录制过程中收到的控件。

这是一个同步控件，不可取消。 没有为此控件定义任何功能。

下表包含使用控件时 [**KSCAMERA \_ EXTENDEDPROP \_ 标头**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_header) 结构字段的说明和要求。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>成员</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>这必须为1。</p></td>
</tr>
<tr class="even">
<td><p>PinId</p></td>
<td><p>这必须是与视频 pin 关联的 Pin ID。</p></td>
</tr>
<tr class="odd">
<td><p>大小</p></td>
<td><p>这必须是 sizeof (KSCAMERA_EXTENDEDPROP_HEADER) + sizeof (KSCAMERA_EXTENDEDPROP_VALUE) 。</p></td>
</tr>
<tr class="even">
<td><p>结果</p></td>
<td><p>指示上一次设置操作的错误结果。 如果未执行任何设置操作，则此必须为0。</p></td>
</tr>
<tr class="odd">
<td><p>功能</p></td>
<td><p>此属性必须为 0。</p></td>
</tr>
<tr class="even">
<td><p>Flags</p></td>
<td><p>这是一个读/写字段。 这可以是上面定义的任何一个标志。</p></td>
</tr>
</tbody>
</table>

## <a name="requirements"></a>要求

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Ksmedia.h</td>
</tr>
</tbody>
</table>
