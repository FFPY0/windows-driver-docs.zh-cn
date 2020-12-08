---
title: SeStopImpersonatingClient 例程
description: SeStopImpersonatingClient 例程结束调用线程的用户模拟。
keywords:
- SeStopImpersonatingClient 例程可安装文件系统驱动程序
topic_type:
- apiref
api_name:
- SeStopImpersonatingClient
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22ee9426fbd6e90fe8258a063f014b867f9aee38
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820743"
---
# <a name="sestopimpersonatingclient-routine"></a>SeStopImpersonatingClient 例程


**SeStopImpersonatingClient** 例程结束调用线程的用户模拟。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
VOID SeStopImpersonatingClient(void);
```

<a name="parameters"></a>参数
----------

此例程没有参数。

<a name="return-value"></a>返回值
------------

无

<a name="remarks"></a>备注
-------

服务器线程可以通过调用 [**SeImpersonateClientEx**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-seimpersonateclientex) 例程来模拟用户。 当线程完成模拟用户时，它将调用 **SeStopImpersonatingClient** 例程来结束模拟。

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
<td align="left"><p>版本</p></td>
<td align="left"><p>在 Windows XP 和更高版本的 Windows 操作系统中可用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Ntifs (包含 Ntifs) </td>
</tr>
<tr class="even">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>PASSIVE_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**SeImpersonateClientEx**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-seimpersonateclientex)

 

