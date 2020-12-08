---
title: SM \_ RemovePersistentBinding 函数
description: SM \_ RemovePersistentBinding 方法删除指定适配器端口的指定 SCSI id 的一个或多个永久性绑定。
keywords:
- SM_RemovePersistentBinding 函数存储设备
topic_type:
- apiref
api_name:
- SM_RemovePersistentBinding
api_location:
- Hbapiwmi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b8f77edbb95cd16527b15814452632ca40a0b7bd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821821"
---
# <a name="sm_removepersistentbinding-function"></a>SM \_ RemovePersistentBinding 函数


SM \_ RemovePersistentBinding 方法删除指定适配器端口的指定 SCSI id 的一个或多个永久性绑定。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void SM_RemovePersistentBinding(
   [in, HBAType("HBA_WWN")] uint8                      HbaPortWWN[8],
   [in, HBAType("HBA_WWN")] uint8                      DomainPortWWN[8],
   [in] uint32                                         EntryCount,
   [in, WmiSizeIs("EntryCount")] MS_SMHBA_BINDINGENTRY Entry[],
   [out, HBA_STATUS_QUALIFIERS] HBA_STATUS             HBAStatus
);
```

<a name="parameters"></a>参数
----------

*HbaPortWWN*   
将删除其持久性绑定的端口的全球名称 (WWN) 。

*DomainPortWWN*   
用于回调的全球名称 (WWN) 。 它是端口 \_ 标识符，它具有 \_ 使用物理光纤通道端口发现的 SMP 端口的任意端口标识符的最小值。 如果未使用物理光纤通道端口发现任何 SMP 端口，则它的值为零。

*EntryCount*   
WMI 提供程序可在 Entry 参数中报告的绑定项的数目。

*条目*   
\_ \_ 用于永久性绑定的 MS SMHBA BINDINGENTRY 类型的列表。

*HBAStatus*   
操作的状态。 有关允许值及其说明的列表，请参阅 [HBA \_ 状态](hba-status.md)。 微型端口驱动程序在 GetPersistentBinding OUT 结构的 HBAStatus 成员中返回此信息 \_ 。

<a name="return-value"></a>返回值
------------

不适用于 WMI 方法。

<a name="remarks"></a>备注
-------

此 WMI 方法属于 MS \_ SM \_ TargetInformationMethods WMI 类。

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
<td align="left">Hbapiwmi</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[HBA \_ 状态](hba-status.md)

[**SM \_ RemovePersistentBinding \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_removepersistentbinding_in)

[**SM \_ RemovePersistentBinding \_**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_sm_removepersistentbinding_out)

 

