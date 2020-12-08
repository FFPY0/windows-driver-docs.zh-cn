---
title: DEVPKEY_DeviceInterfaceClass_DefaultInterface
description: DEVPKEY_DeviceInterfaceClass_DefaultInterface
keywords:
- DEVPKEY_DeviceInterfaceClass_DefaultInterface 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceInterfaceClass_DefaultInterface
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1138e9e6805113df64743d01dc37d9198d9c68a2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841247"
---
# <a name="devpkey_deviceinterfaceclass_defaultinterface"></a>DEVPKEY_DeviceInterfaceClass_DefaultInterface


DEVPKEY_DeviceInterfaceClass_DefaultInterface 设备属性表示设备接口类的默认设备接口的符号链接名称。

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
<td align="left"><p>DEVPKEY_DeviceInterfaceClass_DefaultInterface</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-string.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING&lt;/strong&gt;](devprop-type-string.md)"><strong>DEVPROP_TYPE_STRING</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>和</strong></p></td>
<td align="left"><p>安装应用程序和安装程序的读取和写入访问权限</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

有关如何安装和使用设备接口的信息，请参阅 [设备接口类](./overview-of-device-interface-classes.md) 和 [**INF AddInterface 指令**](./inf-addinterface-directive.md)。

可以通过调用 [**SetupDiGetDeviceInterfaceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdeviceinterfacepropertyw)来检索 DEVPKEY_DeviceInterfaceClass_DefaultInterface 的值。 可以通过调用 [**SetupDiSetDeviceInterfaceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdisetdeviceinterfacepropertyw)来设置 DEVPKEY_DeviceInterfaceClass_DefaultInterface。

Windows Server 2003、Windows XP 和 Windows 2000 支持此属性，但不支持 DEVPKEY_DeviceInterfaceClass_DefaultInterface 属性键。 有关如何在这些早期版本的 Windows 上访问设备接口类的默认接口的信息，请参阅 [访问设备接口类属性](./accessing-device-interface-class-properties.md)。

<a name="requirements"></a>要求
------------

**版本**： windows Vista 和更高版本的 windows **标题**： Devpkey (包含 Devpkey) 


## <a name="see-also"></a>请参阅


[**INF AddInterface 指令**](./inf-addinterface-directive.md)

[**SetupDiGetClassDevs**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclassdevsw)

[**SetupDiGetDeviceInterfaceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdeviceinterfacepropertyw)

[**SetupDiSetDeviceInterfaceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdisetdeviceinterfacepropertyw)

 

