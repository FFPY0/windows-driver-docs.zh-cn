---
title: RemoveLink 函数
description: RemoveLink WMI 方法配置 WMI 提供程序，使其停止向 WMI 客户端传递 fabric 链接事件信息。
keywords:
- RemoveLink 函数存储设备
topic_type:
- apiref
api_name:
- RemoveLink
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b4ae377f0cbf7f298538a1470ba81ef561d6af80
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811417"
---
# <a name="removelink-function"></a>RemoveLink 函数


**RemoveLink** wmi 方法配置 wmi 提供程序，使其停止向 WMI 客户端传递 fabric 链接事件信息。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void RemoveLink(
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus
);
```

<a name="parameters"></a>参数
----------

*HBAStatus*   
返回时，包含操作的状态。 有关允许值及其说明的列表，请参阅 [HBA \_ 状态](hba-status.md)。 微型端口驱动程序在 [**RemoveLink \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_removelink_out)结构的 **HBAStatus** 成员中返回此信息。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

<a name="remarks"></a>备注
-------

此 WMI 方法属于 [MSFC \_ EventControl WMI 类](msfc-eventcontrol-wmi-class.md)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>目标平台</p></td>
<td align="left">台式机</td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left"> (包含 Hbapiwmi、Hbaapi 或 Hbaapi 的 Hbapiwmi) </td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**RemoveLink \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_removelink_out)

 

