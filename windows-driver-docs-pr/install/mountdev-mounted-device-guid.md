---
title: MOUNTDEV_MOUNTED_DEVICE_GUID
description: MOUNTDEV_MOUNTED_DEVICE_GUID
keywords:
- MOUNTDEV_MOUNTED_DEVICE_GUID 设备和驱动程序安装
topic_type:
- apiref
api_name:
- MOUNTDEV_MOUNTED_DEVICE_GUID
api_location:
- Mountmgr.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c1b1f9cdc4adef6cbeb6df165cf41870ca34a816
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824059"
---
# <a name="mountdev_mounted_device_guid"></a>MOUNTDEV_MOUNTED_DEVICE_GUID


为卷设备定义 MOUNTDEV_MOUNTED_DEVICE_GUID [设备接口类](./overview-of-device-interface-classes.md) 。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Attribute</th>
<th align="left">设置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>标识符</p></td>
<td align="left"><p>MOUNTDEV_MOUNTED_DEVICE_GUID</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{53F5630D-B6BF-11D0-94F2-00A0C91EFB8B}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

此设备接口类的 MOUNTDEV_MOUNTED_DEVICE_GUID 标识符是 [**GUID_DEVINTERFACE_VOLUME**](guid-devinterface-volume.md) 设备接口类的别名。

WDK 中的存储 [示例](https://go.microsoft.com/fwlink/p/?LinkId=618052) 包括 [ClassPnP 存储类驱动程序库，该程序库](/samples/browse/) 使用 MOUNTDEV_MOUNTED_DEVICE_GUID 来注册 GUID_DEVINTERFACE_VOLUME 设备接口类的实例。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Mountmgr (包含 Mountmgr) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**GUID_DEVINTERFACE_VOLUME**](guid-devinterface-volume.md)

