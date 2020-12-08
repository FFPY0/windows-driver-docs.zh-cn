---
title: DEVPKEY_Device_ContainerId
description: DEVPKEY_Device_ContainerId
keywords:
- DEVPKEY_Device_ContainerId 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_ContainerId
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 15c3bddad913cdc26ffe42f64a3242ddba8d2e32
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840077"
---
# <a name="devpkey_device_containerid"></a>DEVPKEY_Device_ContainerId


即插即用 (PnP) 管理器使用 DEVPKEY_Device_ContainerId 设备属性将一个或多个设备节点 (*devnodes*) 分组到表示物理设备实例的 *设备容器* 。

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
<td align="left"><p>DEVPKEY_Device_ContainerId</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><a href="devprop-type-guid.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_GUID&lt;/strong&gt;](devprop-type-guid.md)"><strong>DEVPROP_TYPE_GUID</strong></a></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>和</strong></p></td>
<td align="left"><p>安装应用程序和安装程序的只读访问</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

从 Windows 7 开始，PnP 管理器使用设备容器及其标识符 (*ContainerID*) 对源自并属于特定物理设备的每个实例的一个或多个 *devnodes* 进行分组。 设备实例的 ContainerID 通过 DEVPKEY_Device_ContainerId 设备属性进行引用。

将源自一个设备实例的所有 devnodes 都分组到容器中时，将完成以下结果：

-   操作系统可以确定功能在源自物理设备的 *devnodes* 之间的关系。

-   用户或应用程序是以设备为中心的设备视图（而不是传统的以函数为中心的视图）提供的。

DEVPKEY_Device_ContainerId 可用于确定系统中 *devnodes* 的设备容器分组。 对于给定的 devnode，可以通过完成以下步骤来确定属于同一容器的所有 devnodes：

-   调用 [**SetupDiGetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdevicepropertyw) 以查询给定 devnode 的 DEVPKEY_Device_ContainerId。 Windows 返回 devnode 所属的设备容器的 ContainerID *GUID* 值。

-   枚举计算机上的所有 devnodes，并查询每个 devnode 的 DEVPKEY_Device_ContainerId。 与原始 devnode 的 ContainerId 值匹配的每个 ContainerId 值都属于同一容器。

**注意**  属于给定总线类型上的容器的所有 *devnodes* 必须共享同一个 ContainerID 值。

 

有关 ContainerIDs 的详细信息，请参阅 [容器 id](./container-ids.md)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>版本</p></td>
<td align="left"><p>在 windows 7 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Devpkey (包含 Devpkey) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[容器 ID](./container-ids.md)

[**SetupDiGetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

