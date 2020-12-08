---
title: 'SpinLockDpc 规则 (wdm) '
description: SpinLockDpc 规则指定对 KeAcquireSpinLock 或 KeAcquireSpinLockRaiseToDpc 和 KeReleaseSpinLock 的调用必须在严格替换中进行。
ms.date: 05/21/2018
keywords:
- 'SpinLockDpc 规则 (wdm) '
topic_type:
- apiref
api_name:
- SpinLockDpc
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e654617d810a47b77f8dcfc4a5a80102d6aa7e71
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810801"
---
# <a name="spinlockdpc-rule-wdm"></a>SpinLockDpc 规则 (wdm) 


**SpinLockDpc** 规则指定对 [**KeAcquireSpinLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock)或 [**KeAcquireSpinLockRaiseToDpc**](/previous-versions/windows/hardware/drivers/ff551928(v=vs.85))和 [**KeReleaseSpinLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock)的调用必须在严格替换中进行。 也就是说，在调用 **KeAcquireSpinLock** 或 **KeAcquireSpinLockRaiseToDpc** 之后，驱动程序必须先调用 **KeReleaseSpinLock** ，然后再调用 **KeAcquireSpinLock** 或 **KeAcquireSpinLockRaiseToDpc**。

而且，在调度或取消例程结束时，驱动程序不应保存旋转锁。

**驱动程序模型： WDM**

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
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>SpinLockDpc</strong> 规则。</p>
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

[**KeAcquireSpinLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keacquirespinlock) 
[**KeAcquireSpinLockRaiseToDpc**](/previous-versions/windows/hardware/drivers/ff551928(v=vs.85)) 
[**KeReleaseSpinLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kereleasespinlock)
