---
title: KSPROPERTY \_ VPCONFIG \_ GETVIDEOFORMAT
description: KSPROPERTY \_ VPCONFIG \_ GETVIDEOFORMAT 属性检索受支持像素格式的数组。
keywords:
- KSPROPERTY_VPCONFIG_GETVIDEOFORMAT 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_VPCONFIG_GETVIDEOFORMAT
api_location:
- ksmedia.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f7f87fd4e0c577726e8d02b6227cf37012f9df2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794173"
---
# <a name="ksproperty_vpconfig_getvideoformat"></a>KSPROPERTY \_ VPCONFIG \_ GETVIDEOFORMAT


KSPROPERTY \_ VPCONFIG \_ GETVIDEOFORMAT 属性检索受支持像素格式的数组。

## <span id="ddk_ksproperty_vpconfig_getvideoformat_ks"></span><span id="DDK_KSPROPERTY_VPCONFIG_GETVIDEOFORMAT_KS"></span>


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
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier" data-raw-source="[&lt;strong&gt;KSPROPERTY&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksidentifier)"><strong>KSPROPERTY</strong></a></p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddpixelformat" data-raw-source="[&lt;strong&gt;DDPIXELFORMAT&lt;/strong&gt;](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddpixelformat)"><strong>DDPIXELFORMAT</strong></a></p></td>
</tr>
</tbody>
</table>

 

 (操作数据) 的属性值是描述视频端口像素格式的 DDPIXELFORMAT 结构。

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

[**DDPIXELFORMAT**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-_ddpixelformat)

