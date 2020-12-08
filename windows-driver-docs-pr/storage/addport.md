---
title: AddPort 函数
description: AddPort WMI 方法将 WMI 提供程序配置为通知 WMI 客户端与所指示的端口关联的事件。
keywords:
- AddPort 函数存储设备
topic_type:
- apiref
api_name:
- AddPort
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: efe962b1499cfddd3fab16b0ee2d748c74f6cf68
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811813"
---
# <a name="addport-function"></a>AddPort 函数


**AddPort** wmi 方法将 wmi 提供程序配置为通知 wmi 客户端与所指示的端口关联的事件。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void AddPort(
   [in, HBAType("HBA_WWN")] uint8          PortWWN[8],
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS HBAStatus
);
```

<a name="parameters"></a>参数
----------

*PortWWN \[ 8\]*   
一个全球名称，用于指示要报告其事件的端口。

*HBAStatus*   
返回时，包含操作的状态。 有关允许值及其说明的列表，请参阅 [HBA \_ 状态](hba-status.md)。 微型端口驱动程序在 [**AddPort \_ OUT**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_addport_out)结构的 **HBAStatus** 成员中返回此信息。

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


[**AddPort \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_addport_in)

[**AddPort \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_addport_out)

 

