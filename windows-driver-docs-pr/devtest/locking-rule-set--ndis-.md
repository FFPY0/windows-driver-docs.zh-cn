---
title: 锁定规则集 (NDIS)
description: 了解如何使用规则 (NDIS) 验证驱动程序是否正确管理共享资源，以及如何选择锁定规则集。
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: 4c366a0c40e6d941bb89f548c252a53b9785394f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819721"
---
# <a name="locking-rule-set-ndis"></a>锁定规则集 (NDIS)


使用这些规则验证驱动程序是否正确管理共享资源。

## <a name="in-this-section"></a>在本节中


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="ndis-spinlock.md" data-raw-source="[&lt;strong&gt;SpinLock&lt;/strong&gt;](ndis-spinlock.md)"><strong>SpinLock</strong></a></p></td>
<td align="left"><p><a href="ndis-spinlock.md" data-raw-source="[&lt;strong&gt;SpinLock&lt;/strong&gt;](ndis-spinlock.md)"><strong>旋转锁</strong></a>规则验证 NDIS 旋转锁定接口的正确使用。 此规则指定仅当旋转锁处于解锁状态时才对 <a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisacquirespinlock" data-raw-source="[&lt;strong&gt;NdisAcquireSpinLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisacquirespinlock)"><strong>NdisAcquireSpinLock</strong></a> 进行调用。 此规则还将验证旋转锁是否在微型端口处理程序例程退出之前被释放。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-spinlockbalanced.md" data-raw-source="[&lt;strong&gt;SpinLockBalanced&lt;/strong&gt;](ndis-spinlockbalanced.md)"><strong>SpinLockBalanced</strong></a></p></td>
<td align="left"><p><a href="ndis-spinlockbalanced.md" data-raw-source="[&lt;strong&gt;SpinLockBalanced&lt;/strong&gt;](ndis-spinlockbalanced.md)"><strong>SpinLockBalanced</strong></a>规则验证对获取旋转锁的函数的调用次数是否等于释放同一旋转锁的函数的调用次数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-spinlockdpr.md" data-raw-source="[&lt;strong&gt;SpinLockDpr&lt;/strong&gt;](ndis-spinlockdpr.md)"><strong>SpinLockDpr</strong></a></p></td>
<td align="left"><p><a href="ndis-spinlockdpr.md" data-raw-source="[&lt;strong&gt;SpinLockDpr&lt;/strong&gt;](ndis-spinlockdpr.md)"><strong>SpinLockDpr</strong></a>规则验证 NDIS 旋转锁定接口的正确使用。</p>
<p>此规则指定仅当旋转锁定处于未锁定状态时才对 <a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisdpracquirespinlock" data-raw-source="[&lt;strong&gt;NdisDprAcquireSpinLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisdpracquirespinlock)"><strong>NdisDprAcquireSpinLock</strong></a> 进行调用。 此规则还验证在微型端口处理程序例程退出之前是否释放自旋锁。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ndis-spinlockdprrelease.md" data-raw-source="[&lt;strong&gt;SpinLockDprRelease&lt;/strong&gt;](ndis-spinlockdprrelease.md)"><strong>SpinLockDprRelease</strong></a></p></td>
<td align="left"><p><a href="ndis-spinlockdprrelease.md" data-raw-source="[&lt;strong&gt;SpinLockDprRelease&lt;/strong&gt;](ndis-spinlockdprrelease.md)"><strong>SpinLockDprRelease</strong></a>规则验证仅当旋转锁为 "未锁定" 状态时，才调用对<a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisacquirespinlock" data-raw-source="[&lt;strong&gt;NdisAcquireSpinLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisacquirespinlock)"><strong>NdisAcquireSpinLock</strong></a>或<a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisdpracquirespinlock" data-raw-source="[&lt;strong&gt;NdisDprAcquireSpinLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisdpracquirespinlock)"><strong>NdisDprAcquireSpinLock</strong></a>的调用。 此规则还检查在退出微型端口处理程序例程之前，旋转锁已释放。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ndis-spinlockrelease.md" data-raw-source="[&lt;strong&gt;SpinLockRelease&lt;/strong&gt;](ndis-spinlockrelease.md)"><strong>SpinLockRelease</strong></a></p></td>
<td align="left"><p>SpinLockRelease 规则指定驱动程序不得在不首先获取旋转锁 (<a href="/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreleasespinlock" data-raw-source="[&lt;strong&gt;NdisReleaseSpinLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisreleasespinlock)"><strong>NdisReleaseSpinLock</strong></a>) 的情况下将其释放。</p></td>
</tr>
</tbody>
</table>

 

**选择锁定规则集**

1.  选择你的驱动程序项目 () 在 Microsoft Visual Studio 中。 在 " **驱动程序** " 菜单中，单击 " **启动静态驱动程序验证程序 ...**"。

2.  单击 " **规则** " 选项卡。在 " **规则集**" 下，选择 " **锁定**"。

    若要从 Visual Studio 开发人员命令提示符窗口中选择默认规则集，请使用 **/check** 选项指定 **sdv** 。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:Locking.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅 [使用静态驱动程序验证器查找驱动程序中的缺陷](./using-static-driver-verifier-to-find-defects-in-drivers.md) 和 [静态驱动程序验证程序命令 (MSBuild) ](./-static-driver-verifier-commands--msbuild-.md)。

