---
title: KSPROPERTY \_ CAMERACONTROL \_ ZOOM \_ 相对
description: KSPROPERTY \_ CAMERACONTROL \_ zoom \_ 相对属性指定相机的缩放状态。
keywords:
- KSPROPERTY_CAMERACONTROL_ZOOM_RELATIVE 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_ZOOM_RELATIVE
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: a2018eced3f989c6c69a2a80d7910ff8405e9318
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821793"
---
# <a name="ksproperty_cameracontrol_zoom_relative"></a>KSPROPERTY \_ CAMERACONTROL \_ ZOOM \_ 相对


KSPROPERTY \_ CAMERACONTROL \_ zoom \_ 相对属性指定相机的缩放状态。

## <span id="ddk_ksproperty_cameracontrol_zoom_relative_ks"></span><span id="DDK_KSPROPERTY_CAMERACONTROL_ZOOM_RELATIVE_KS"></span>


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
<td><p>筛选器或节点</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s)"><strong>KSPROPERTY_CAMERACONTROL_S</strong></a>或<a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_NODE_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s)"> <strong>KSPROPERTY_CAMERACONTROL_NODE_S</strong></a></p></td>
<td><p>LONG</p></td>
</tr>
</tbody>
</table>

 

) 操作数据 (的属性值是指定相机的相对缩放设置的 LONG。 值的大小表示所需的缩放速度;较高的值表示较高的速度。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>“值”</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>0</p></td>
<td><p>停止缩放镜头运动。</p></td>
</tr>
<tr class="even">
<td><p>正值</p></td>
<td><p>开始在 telephoto 方向上移动缩放镜头 (启动) 的放大。</p></td>
</tr>
<tr class="odd">
<td><p>负值</p></td>
<td><p>开始在广角方向上移动缩放镜头 (启动缩小) 。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

[**KSPROPERTY \_ CAMERACONTROL \_ 节点 \_**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s)结构的 **值** 成员指定了相对缩放。

请注意，特定设备可能仅支持特定的速度范围。 若要确定设备支持的速度范围，应用程序可以发出 KSPROPERTY \_ 类型 \_ BASICSUPPORT 请求。 可以 \_ \_ 在 [**KSPROPERTY \_ 项**](/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_item)结构的 **Flags** 成员中指定 KSPROPERTY 类型 BASICSUPPORT。

某些设备仅支持一个缩放速度。 在这种情况下， **值** 成员的符号指示该镜头应放大还是缩小。

发出集请求时，客户端应提供 KSPROPERTY CAMERACONTROL 节点的 **值** 成员的上一个表中的值之一 \_ \_ \_ 。

发出 get 请求时，客户端将接收 KSPROPERTY **Value** \_ CAMERACONTROL \_ 节点 S 结构的值成员中前一个表中的值之一 \_ 。 值指示照相机的当前缩放状态。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>适用于 windows Vista 和更高版本的 Windows 操作系统。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ksmedia (包含 Ksmedia) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**KSPROPERTY \_ CAMERACONTROL \_ 节点 \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s)

