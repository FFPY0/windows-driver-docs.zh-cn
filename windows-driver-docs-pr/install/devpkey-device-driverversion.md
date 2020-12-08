---
title: DEVPKEY_Device_DriverVersion
description: DEVPKEY_Device_DriverVersion
keywords:
- DEVPKEY_Device_DriverVersion 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_DriverVersion
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 53a864508748a7b4151ee2e663efa8bd1dc10586
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798139"
---
# <a name="devpkey_device_driverversion"></a>DEVPKEY_Device_DriverVersion


PKEY_Device_DriverVersion 设备属性表示设备实例上当前安装的驱动程序的版本。

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
<td align="left"><p>DEVPKEY_Device_DriverVersion</p></td>
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
<td align="left"><p><strong>对应的注册表值标识符和注册表值名称</strong></p></td>
<td align="left"><p>REGSTR_VAL_DRIVERVERSION</p>
<p><strong>DriverVersion</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

DEVPKEY_Device_DriverVersion 的值是由 inf [**DriverVer 指令**](./inf-driverver-directive.md)提供的，inf 版本部分包括在安装设备的 inf [**版本部分**](./inf-version-section.md)中，或由安装设备的 [**inf *DDInstall* 部分**](./inf-ddinstall-section.md)中包含的特定于设备的 inf **DriverVer** 指令提供。

可以调用 [**SetupDiGetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdevicepropertyw) 来检索 PKEY_Device_DriverVersion 的值。

Windows Server 2003、Windows XP 和 Windows 2000 支持此属性，但不支持 DEVPKEY_Device_DriverVersion 属性键。 在这些早期版本的 Windows 上，可以通过访问设备实例的软件密钥下的相应 **DriverVersion** 注册表值来访问此属性的值。 有关如何在这些早期版本的 Windows 上访问此属性值的信息，请参阅 [访问设备驱动程序属性](./accessing-device-driver-properties.md)。

<a name="requirements"></a>要求
------------

**版本**： windows Vista 和更高版本的 windows **标题**： Devpkey (包含 Devpkey) 


## <a name="see-also"></a>请参阅


[**INF *DDInstall* 部分**](./inf-ddinstall-section.md)

[**INF DriverVer 指令**](./inf-driverver-directive.md)

[**INF Version 节**](./inf-version-section.md)

[**SetupDiGetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

