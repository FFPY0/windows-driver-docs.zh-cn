---
title: 'SpIrql 规则 (storport) '
description: 此规则验证例程 TdiRegisterPnPHandlers 和 TdiDeregisterPnPHandlers 仅在 IRQL 低于调度级别的情况下调用 \_ 。 但是，如果调用 ExFreeToNPagedLookasideList，则规则通过。
ms.date: 05/21/2018
keywords:
- 'SpIrql 规则 (storport) '
topic_type:
- apiref
api_name:
- SpIrql
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e16eaea33d94493f9ff38ad67a4fdff8ff3071ad
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828153"
---
# <a name="spirql-rule-storport"></a>SpIrql 规则 (storport) 


此规则验证例程 **TdiRegisterPnPHandlers** 和 **TDIDEREGISTERPNPHANDLERS** 仅在 IRQL 低于 **调度 \_ 级别** 的情况下调用。 但是，如果调用 **ExFreeToNPagedLookasideList** ，则规则通过。

**驱动程序模型： Storport**

<a name="how-to-test"></a>如何测试
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在编译时</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>SpIrql</strong> 规则。</p>
使用以下步骤来运行代码分析：
<ol>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](./using-static-driver-verifier-to-find-defects-in-drivers.md#preparing-your-source-code)">准备你的代码 (使用) 的角色类型声明。</a></li>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](./using-static-driver-verifier-to-find-defects-in-drivers.md#running-static-driver-verifier)">运行静态驱动程序验证程序。</a></li>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](./using-static-driver-verifier-to-find-defects-in-drivers.md#viewing-and-analyzing-the-results)">查看并分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅 <a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](./using-static-driver-verifier-to-find-defects-in-drivers.md)">使用静态驱动程序验证器查找驱动程序中的缺陷</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用于
----------

[**ExFreeToNPagedLookasideList**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exfreetonpagedlookasidelist)
