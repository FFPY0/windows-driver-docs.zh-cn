---
title: KSPROPERTY \_ CAMERACONTROL \_ IMAGE \_ 引脚 \_ 功能 \_ 属性
description: 用户模式客户端使用此属性来确定照相机的图像 pin 和记录 pin 是否互相排斥。 如果它们互相排斥，则当记录插针处于活动状态时，图像插针不能处于活动状态，反之亦然。
keywords:
- KSPROPERTY_CAMERACONTROL_IMAGE_PIN_CAPABILITY_PROPERTY 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_IMAGE_PIN_CAPABILITY_PROPERTY
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0d32d4c5b7c417d88f826fc12ee926deaa0caa51
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840553"
---
# <a name="ksproperty_cameracontrol_image_pin_capability_property"></a>KSPROPERTY \_ CAMERACONTROL \_ IMAGE \_ 引脚 \_ 功能 \_ 属性


用户模式客户端使用此属性来确定照相机的图像 pin 和记录 pin 是否互相排斥。 如果它们互相排斥，则当记录插针处于活动状态时，图像插针不能处于活动状态，反之亦然。

## <span id="ddk_ksproperty_cameracontrol_pan_ks"></span><span id="DDK_KSPROPERTY_CAMERACONTROL_PAN_KS"></span>


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
<td><p>筛选器</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_image_pin_capability_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_IMAGE_PIN_CAPABILITY_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_image_pin_capability_s)"><strong>KSPROPERTY_CAMERACONTROL_IMAGE_PIN_CAPABILITY_S</strong></a></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

如果驱动程序实现此属性并且标识图像 pin 专用于记录 pin，则在记录发生时，媒体流式处理管道会阻止 "拍摄照片" 命令进入驱动程序。

## <a name="see-also"></a>请参阅


[**KSPROPERTY**](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)

[**KSPROPERTY \_ CAMERACONTROL \_ 图像 \_ PIN \_ 功能 \_**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_image_pin_capability_s)

