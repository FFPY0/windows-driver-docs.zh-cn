---
title: KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ FACEAUTH \_ 模式
description: KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ FACEAUTH \_ 模式是用于打开和关闭人脸身份验证的属性 ID。
keywords:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FACEAUTH_MODE 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_EXTENDED_FACEAUTH_MODE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 09/10/2018
ms.localizationpriority: medium
ms.openlocfilehash: faa866deb22845e134318534641e50c753ef26bb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821195"
---
# <a name="ksproperty_cameracontrol_extended_faceauth_mode"></a>KSPROPERTY \_ CAMERACONTROL \_ 扩展 \_ FACEAUTH \_ 模式


**KSPROPERTY \_CAMERACONTROL \_ 扩展 \_ FACEAUTH \_ 模式** 是用于打开和关闭人脸身份验证的属性 ID。

### <a name="usage-summary-table"></a>使用情况摘要表

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

 

以下位标志控制驱动程序中的人脸身份验证：

```cpp
#define KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_DISABLED                        0x0000000000000001
#define KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_ALTERNATIVE_FRAME_ILLUMINATION  0x0000000000000002
#define KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_BACKGROUND_SUBTRACTION          0x0000000000000004
```

下表描述了标志功能：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>标志</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_DISABLED</strong></p></td>
<td><p>可选功能。</p>
<p>指定时，驱动程序将禁用视频外观身份验证模式。 此标志与 <strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_BACKGROUND_SUBTRACTION</strong> 和 <strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_ALTERNATIVE_FRAME_ILLUMINATION</strong> 标志互斥。</p></td>
</tr>
<tr class="even">
<td><p><strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_ALTERNATIVE_FRAME_ILLUMINATION</strong></p></td>
<td><p>如果 <strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_BACKGROUND_SUBTRACTION</strong> 不受支持，则为必需的功能。</p>
<p>如果指定此项，则必须在每个示例上设置 <strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_ALTERNATIVE_FRAME_ILLUMINATION</strong> ，如框架元数据所述。 此标志与 <strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_BACKGROUND_SUBTRACTION</strong> 和 <strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_DISABLED</strong> 标志互斥。 在此模式下，应在捕获的每个帧上打开/关闭备用 IR 闪光。</p></td>
</tr>
<tr class="odd">
<td><p><strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_BACKGROUND_SUBTRACTION</strong></p></td>
<td><p>如果 <strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_ALTERNATIVE_FRAME_ILLUMINATION</strong> 不受支持，则为必需的功能。</p>
<p>此标志与 <strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_ALTERNATIVE_FRAME_ILLUMINATION</strong> 和 <strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_DISABLED</strong> 标志互斥。 在此模式下，应创建具有背景环境红外轻型的 IR 映像。</p></td>
</tr>
</tbody>
</table>

 

默认情况下，如果是常规用途 IR 相机，则驱动程序应将 **KSPROPERTY \_ CAMERACONTROL \_ EXTENDED \_ FACEAUTH \_ 模式** 设置为 " **KSCAMERA \_ EXTENDEDPROP \_ FACEAUTH \_ mode \_ DISABLED** "。 否则，它应设置为 **KSCAMERA \_ EXTENDEDPROP \_ FACEAUTH \_ 模式 \_ 背景 \_ 减法** 或 **KSCAMERA \_ EXTENDEDPROP \_ FACEAUTH \_ 模式 \_ 备用 \_ 帧 \_ 照明**。

如果要使用 Windows Hello 以外的一般方案，红外相机应播发 **KSCAMERA \_ EXTENDEDPROP \_ FACEAUTH \_ 模式 \_** 。

用于人脸登录的 IR 相机应支持 **KSCAMERA \_ EXTENDEDPROP \_ FACEAUTH \_ 模式 \_ 备用 \_ 帧 \_ 照明** 或 **KSCAMERA \_ EXTENDEDPROP \_ FACEAUTH \_ 模式 \_ 背景 \_ 减** 功能它们只支持其中一个标志。

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
<td><p>只能在筛选器上的一个 pin 上播发。 Pin 必须为类型 <strong>PINNAME_VIDEO_CAPTURE</strong> 或 <strong>PINNAME_VIDEO_PREVIEW</strong>，必须生成 IR 传感器数据，并将其标记为可共享 FrameServer。</p></td>
</tr>
<tr class="odd">
<td><p>大小</p></td>
<td><p>这必须是 <strong>sizeof</strong> (<strong>KSCAMERA_EXTENDEDPROP_HEADER</strong>) + <strong>sizeof</strong> (<a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting" data-raw-source="[&lt;strong&gt;KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagkscamera_extendedprop_videoprocsetting)"><strong>KSCAMERA_EXTENDEDPROP_VIDEOPROCSETTING</strong></a>) 。</p></td>
</tr>
<tr class="even">
<td><p>结果</p></td>
<td><p>指示上一次设置操作的错误结果。 如果未执行任何设置操作，则此必须为0。</p></td>
</tr>
<tr class="odd">
<td><p>功能</p></td>
<td><p>必须是前面定义的 <strong>KSCAMERA_EXTENDEDPROP_ FACEAUTH_MODE_xxx</strong> 标志的一个比特或。</p>
<p>驱动程序不应同时播发 <strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_ALTERNATIVE_FRAME_ILLUMINATION</strong> 和 <strong>KSCAMERA_EXTENDEDPROP_FACEAUTH_MODE_BACKGROUND_SUBTRACTION</strong></p></td>
</tr>
<tr class="even">
<td><p>Flags</p></td>
<td><p>这是一个读/写字段。 这可以是上面定义的 <strong>KSCAMERA_EXTENDEDPROP_ FACEAUTH_MODE_xxx</strong> 标志之一。</p></td>
</tr>
</tbody>
</table>

 

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
<td>Ksmedia.h</td>
</tr>
</tbody>
</table>
