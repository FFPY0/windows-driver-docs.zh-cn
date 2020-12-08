---
title: 'PnpRemove 规则 (wdm) '
description: PnpRemove 规则指定驱动程序无法完成 IRP \_ MN \_ 意外 \_ 删除、irp \_ MN \_ 取消 \_ 删除 \_ 设备、irp \_ MN \_ cancel \_ 停止 \_ 设备或 irp \_ MN \_ 删除 \_ 设备请求失败。
ms.date: 05/21/2018
keywords:
- 'PnpRemove 规则 (wdm) '
topic_type:
- apiref
api_name:
- PnpRemove
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e9511fb947a0196bce1965b51d06aaf59b1402ce
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810989"
---
# <a name="pnpremove-rule-wdm"></a>PnpRemove 规则 (wdm) 


**PnpRemove** 规则指定驱动程序无法完成 IRP \_ MN \_ 意外 \_ 删除、irp \_ MN \_ 取消 \_ 删除 \_ 设备、irp \_ MN \_ cancel \_ 停止 \_ 设备或 irp \_ MN \_ 删除 \_ 设备请求失败。

> [!NOTE]
> 在 Windows 8.1 中，可以使用 [驱动程序验证程序](./driver-verifier.md)测试 **PnpRemove** 规则。 此规则当前不可用于 [静态驱动程序验证程序](./static-driver-verifier.md)。

 

**驱动程序模型： WDM**

**Bug 检查 () 发现此规则**： [**bug 检查0XC4：驱动程序 \_ 验证器 \_ 检测到 \_ 违反**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md) (0x00043006) 


<a name="how-to-test"></a>如何测试
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在运行时</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](./driver-verifier.md)">驱动程序验证程序</a> ，并选择 " <a href="/windows-hardware/drivers/devtest/ddi-compliance-checking" data-raw-source="[DDI compliance checking](./ddi-compliance-checking.md)">DDI 相容性检查</a> " 选项。</p></td>
</tr>
</tbody>
</table>

 

