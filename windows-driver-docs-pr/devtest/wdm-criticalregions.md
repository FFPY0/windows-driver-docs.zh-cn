---
title: 'CriticalRegions 规则 (wdm) '
description: CriticalRegions 规则指定在调用 KeLeaveCriticalRegion 之前驱动程序必须调用 KeEnterCriticalRegion，并且驱动程序会在对 KeEnterCriticalRegion 的任何后续调用之前调用 KeLeaveCriticalRegion。 允许 (嵌套调用。 ) 。
ms.date: 05/21/2018
keywords:
- 'CriticalRegions 规则 (wdm) '
topic_type:
- apiref
api_name:
- CriticalRegions
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 665c639daf70581da79a5faf3fd66d2de966e224
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832489"
---
# <a name="criticalregions-rule-wdm"></a>CriticalRegions 规则 (wdm) 


**CriticalRegions** 规则指定在调用 [**KeLeaveCriticalRegion**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleavecriticalregion)之前驱动程序必须调用 [**KeEnterCriticalRegion**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion) ，并且驱动程序会在对 **KeEnterCriticalRegion** 的任何后续调用之前调用 **KeLeaveCriticalRegion** 。 允许 (嵌套调用。 ) 

此规则还指定驱动程序调用 **KeLeaveCriticalRegion** ，以便在其返回之前，重新启用 (apc) 的常规内核异步过程调用。

**KeEnterCriticalRegion** 和 **KeLeaveCriticalRegion** 的 WDK 文档说明了这些函数的调用方可以以 IRQL &lt; = APC \_ 级别运行。 在这种情况下，此规则将强制实施最佳做法建议。

**驱动程序模型： WDM**

**Bug 检查 () 发现此规则**： [**bug 检查0XC4：驱动程序 \_ 验证器 \_ 检测到 \_ 违反**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md) (0x00040003) 


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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>CriticalRegions</strong> 规则。</p>
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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](./driver-verifier.md)">驱动程序验证程序</a> ，并选择 " <a href="/windows-hardware/drivers/devtest/ddi-compliance-checking#ddi-compliance-checking-additional" data-raw-source="[DDI compliance checking (additional)](./ddi-compliance-checking.md#ddi-compliance-checking-additional)">DDI 相容性检查" (其他) </a> 选项。</p></td>
</tr>
</tbody>
</table>

 

<a name="applies-to"></a>适用于
----------

[**ExEnterCriticalRegionAndAcquireResourceExclusive**](/previous-versions/windows/hardware/drivers/dn308550(v=vs.85)) 
[**ExReleaseResourceAndLeaveCriticalRegion**](/previous-versions/windows/hardware/drivers/dn308551(v=vs.85)) 
[**KeEnterCriticalRegion**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion) 
[**KeLeaveCriticalRegion**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keleavecriticalregion)
