---
title: DEVPKEY_Device_DeviceDesc
description: DEVPKEY_Device_DeviceDesc
keywords:
- DEVPKEY_Device_DeviceDesc 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_DeviceDesc
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 00a12b0d80fd00132a37d3ba626b119db155a13f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840075"
---
# <a name="devpkey_device_devicedesc"></a>DEVPKEY_Device_DeviceDesc


DEVPKEY_Device_DeviceDesc 设备属性表示设备实例的说明。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr>
<th>Attribute</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_Device_DeviceDesc</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-string.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING&lt;/strong&gt;](devprop-type-string.md)"><strong>DEVPROP_TYPE_STRING</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>和</strong></p></td>
<td align="left"><p>安装应用程序和安装程序的只读访问</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>对应 SPDRP_</strong><em>Xxx</em> <strong>标识符</strong></p></td>
<td align="left"><p>SPDRP_DEVICEDESC</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>是</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

DEVPKEY_Device_DeviceDesc 的值由安装设备的 INF 文件的 " [**Inf 模型" 部分**](./inf-models-section.md)提供的 *设备说明* 条目值设置。

可以调用 [**SetupDiGetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdevicepropertyw) 来检索 DEVPKEY_DEVICE_DeviceDesc 的值。

可以检索 " [**DEVPKEY_NAME**](devpkey-name--device-instance-.md) 设备实例" 属性的值，以检索设备在用户界面项中应出现的名称。

Windows Server 2003、Windows XP 和 Windows 2000 支持此属性，但不支持 DEVPKEY_Device_DeviceDesc 属性键。 相反，这些早期版本的 Windows 将使用相应的 SPDRP_DEVICEDESC 标识符来访问属性的值。 有关如何在这些早期版本的 Windows 上访问此属性值的信息，请参阅 [SPDRP_Xxx 属性访问设备实例](./accessing-device-instance-spdrp-xxx-properties.md)。

<a name="requirements"></a>要求
------------

**版本**： windows Vista 和更高版本的 windows **标题**： Devpkey (包含 Devpkey) 


## <a name="see-also"></a>请参阅


[**DEVPKEY_NAME（设备实例）**](devpkey-name--device-instance-.md)

[**INF Models 节**](./inf-models-section.md)

[**SetupDiGetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

