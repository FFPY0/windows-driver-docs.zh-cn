---
title: KSPROPERTY \_ PIN \_ 通信
description: KSPROPERTY \_ pin \_ 通信属性指定由 pin 工厂实例化的引脚上的 IRP 流的方向。
keywords:
- KSPROPERTY_PIN_COMMUNICATION 流媒体设备
topic_type:
- apiref
api_name:
- KSPROPERTY_PIN_COMMUNICATION
api_location:
- ks.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: d300475b3b1b4b3b139776156843666a00339ba0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833969"
---
# <a name="ksproperty_pin_communication"></a>KSPROPERTY \_ PIN \_ 通信


KSPROPERTY \_ pin \_ 通信属性指定由 pin 工厂实例化的引脚上的 IRP 流的方向。

## <span id="ddk_ksproperty_pin_communication_ks"></span><span id="DDK_KSPROPERTY_PIN_COMMUNICATION_KS"></span>


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
<td><p><a href="/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin" data-raw-source="[&lt;strong&gt;KSP_PIN&lt;/strong&gt;](/windows-hardware/drivers/ddi/ks/ns-ks-ksp_pin)"><strong>KSP_PIN</strong></a></p></td>
<td><p>KSPIN_COMMUNICATION</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

KS 筛选器返回以下值之一，该值指定此 pin 工厂实例化的 pin 的通信方向：

<span id="KSPIN_COMMUNICATION_NONE"></span><span id="kspin_communication_none"></span>\_无通信 \_ KSPIN  
Pin 工厂不会实例化任何 pin。

<span id="KSPIN_COMMUNICATION_SINK"></span><span id="kspin_communication_sink"></span>KSPIN \_ 通信 \_ 接收器  
Pin 工厂实例化 IRP 接收器 pin。 此类 pin 只能连接到 IRP 源 pin。

<span id="KSPIN_COMMUNICATION_SOURCE"></span><span id="kspin_communication_source"></span>KSPIN \_ 通信 \_ 源  
Pin 工厂实例化 IRP 源 pin。 此类 pin 只能连接到 IRP 接收器 pin。

<span id="KSPIN_COMMUNICATION_BOTH"></span><span id="kspin_communication_both"></span>KSPIN \_ 通信 \_  
Pin 工厂实例化两个均为 IRP 接收器和 IRP 源的 pin。

<span id="KSPIN_COMMUNICATION_BRIDGE"></span><span id="kspin_communication_bridge"></span>KSPIN \_ 通信 \_ 桥  
此 pin 无法连接到其他 pin，但可在其上创建实例以接收非 KS i/o 请求。

源 pin 将 Irp 发送到接收器 pin。 源 pin 可以读取或写入数据，而接收器 pin 可能会从中读取或写入数据。 有关详细信息，请参阅 [**KSPROPERTY \_ PIN \_ 数据流**](ksproperty-pin-dataflow.md)。

Stream 微型驱动程序不需要直接处理此属性;流类驱动程序使用流请求块处理此属性，以便在必要时查询详细信息。

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


[**KSPROPERTY \_ PIN \_ 数据流**](ksproperty-pin-dataflow.md)

