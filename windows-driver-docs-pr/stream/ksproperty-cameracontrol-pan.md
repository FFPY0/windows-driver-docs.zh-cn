---
title: KSPROPERTY \_ CAMERACONTROL \_ 平移
description: 用户模式客户端使用 KSPROPERTY \_ CAMERACONTROL \_ 平移属性来获取或设置照相机的平移设置。 此属性是可选的。
keywords:
- KSPROPERTY_CAMERACONTROL_PAN 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_CAMERACONTROL_PAN
api_location:
- Ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: acea4b0368c7823e5fa75ffee19731f72f55bcc2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840545"
---
# <a name="ksproperty_cameracontrol_pan"></a>KSPROPERTY \_ CAMERACONTROL \_ 平移


用户模式客户端使用 KSPROPERTY \_ CAMERACONTROL \_ 平移属性来获取或设置照相机的平移设置。 此属性是可选的。

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
<td><p>是</p></td>
<td><p>筛选器或节点</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s)"><strong>KSPROPERTY_CAMERACONTROL_S</strong></a>或<a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s" data-raw-source="[&lt;strong&gt;KSPROPERTY_CAMERACONTROL_NODE_S&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_node_s)"> <strong>KSPROPERTY_CAMERACONTROL_NODE_S</strong></a></p></td>
<td><p>LONG</p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是指定相机平移设置的 LONG 值。 此值以度为单位表示。

正值表示相机旋转。 负值表示相机旋转，如下图所示。

![显示照相机平移值的插图](images/cam-pan-1.png)

支持此属性的每个视频捕获微型驱动程序都必须为此属性定义一个范围和默认值。 设备的范围必须是-180 到 + 180。 默认值必须为0。

**警告**  在编写或测试应用程序时，应注意，在实践中，某些驱动程序定义了一系列自定义的平移值和自定义步骤值，这些值可能不基于典型单位。 驱动程序可能会以物理方式或数字方式实现平移控件。

 

<a name="remarks"></a>备注
-------

KSPROPERTY **Value** \_ CAMERACONTROL S 结构的 Value 成员 \_ 指定平移设置。

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

[**KSPROPERTY \_ CAMERACONTROL \_ S**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksproperty_cameracontrol_s)

