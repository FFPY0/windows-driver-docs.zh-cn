---
title: RDBSS 定义的宏
description: RDBSS 定义的宏
keywords:
- RDBSS WDK 文件系统，宏
- 重定向驱动器缓冲子系统 WDK 文件系统，宏
- 宏 WDK RDBSS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4a0ee0265e866971ea7b5d44553fab69f2555fff
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828765"
---
# <a name="macros-defined-by-rdbss"></a>RDBSS 定义的宏


## <span id="ddk_macros_defined_by_rdbss_if"></span><span id="DDK_MACROS_DEFINED_BY_RDBSS_IF"></span>


Windows 驱动程序工具包 (WDK) 头文件中定义了许多有用的宏，用于调用这些 RDBSS 例程或其他内核例程。 通常使用其中的某些宏，而不是直接调用 RDBSS 例程。 其中一些宏用作便利例程。

以下宏由 RDBSS 定义。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">宏</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>RxAcquirePrefixTableLockExclusive</strong> (<em>表</em>， <em>等待</em>) </p></td>
<td align="left"><p>此宏获取用于更改操作的独占模式下的前缀表锁。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxAcquirePrefixTableLockShared</strong> (<em>表</em>， <em>等待</em>) </p></td>
<td align="left"><p>此宏获取用于查找操作的共享模式下的前缀表锁。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxAllocatePoolWithTag</strong> (<em>类型</em>、 <em>大小</em>、 <em>标记</em>) </p></td>
<td align="left"><p>在选中的生成上，此宏从池中分配包含四个字节标记的池中的内存，该标记可用于帮助捕获内存 trashing 的实例。</p>
<p>在零售版上，此宏会直接调用 <a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag" data-raw-source="[&lt;strong&gt;ExAllocatePoolWithTag&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-exallocatepoolwithtag)"><strong>ExAllocatePoolWithTag</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxCheckMemoryBlock</strong> (<em>ptr</em>) </p></td>
<td align="left"><p>在选中的生成上，此宏会检查内存块中是否有特殊的 RX_POOL_HEADER 标头签名。</p>
<p>在零售版上，此宏不执行任何操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxDereferenceAndFinalizeNetFcb</strong> (<em>Fcb、RxContext</em>、 <em>RecursiveFinalize</em>、 <em>ForceFinalize</em>) </p></td>
<td align="left"><p>此宏用于跟踪对 FCB 结构的取消引用操作。</p>
<p>请注意，此宏操作引用计数，同时返回最终取消引用调用的状态。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxDereferenceNetFcb</strong> (<em>Fcb</em>) </p></td>
<td align="left"><p>此宏用于跟踪对 FCB 结构的取消引用操作。</p>
<p>请注意，此宏操作引用计数，同时返回最终取消引用调用的状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxDereferenceNetFobx</strong> (<em>Fobx，LockHoldingState</em>) </p></td>
<td align="left"><p>此宏用于跟踪对 FOBX 结构的取消引用操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxDereferenceNetRoot</strong> (<em>NetRoot</em>， <em>LockHoldingState</em>) </p></td>
<td align="left"><p>此宏用于跟踪对 NET_ROOT 结构的取消引用操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxDereferenceSrvCall</strong> (<em>SrvCall</em>， <em>LockHoldingState</em>) </p></td>
<td align="left"><p>此宏用于跟踪对 SRV_CALL 结构的取消引用操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxDereferenceSrvOpen</strong> ( <em>SrvOpen</em>， <em>LockHoldingState</em>) </p></td>
<td align="left"><p>此宏用于跟踪对 SRV_OPEN 结构的取消引用操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxDereferenceVNetRoot</strong> ( <em>VNetRoot</em>， <em>LockHoldingState</em>) </p></td>
<td align="left"><p>此宏用于跟踪对 V_NET_ROOT 结构的取消引用操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxFcbAcquiredShared</strong> (<em>RXCONTEXT</em>， <em>FCB</em>) </p></td>
<td align="left"><p>此宏检查当前线程是否有权访问共享模式下的常规资源。 此宏调用 <a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredsharedlite" data-raw-source="[&lt;strong&gt;ExIsResourceAcquiredSharedLite&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredsharedlite)"><strong>ExIsResourceAcquiredSharedLite</strong></a> 例程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxFillAndInstallFastIoDispatch</strong> (<em>__devobj</em>， <em>__fastiodisp</em>) </p></td>
<td align="left"><p>此宏调用 <a href="/windows-hardware/drivers/ddi/mrx/nf-mrx-__rxfillandinstallfastiodispatch" data-raw-source="[&lt;strong&gt;__RxFillAndInstallFastIoDispatch&lt;/strong&gt;](/windows-hardware/drivers/ddi/mrx/nf-mrx-__rxfillandinstallfastiodispatch)"><strong>__RxFillAndInstallFastIoDispatch</strong></a> 来填写快速 i/o 调度向量，使其与正常调度 i/o 向量相同，并将其安装到与传递的设备对象关联的驱动程序对象中。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxFreePool</strong> (<em>ptr</em>) </p></td>
<td align="left"><p>在选中的生成上，此宏释放内存池。</p>
<p>在零售版上，此宏会直接调用 <a href="/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool" data-raw-source="[&lt;strong&gt;ExFreePool&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-exfreepool)"><strong>ExFreePool</strong></a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxIsFcbAcquiredShared</strong> (<em>FCB</em>) </p></td>
<td align="left"><p>此宏检查当前线程是否有权访问共享模式下的常规资源。 此宏调用 <a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredsharedlite" data-raw-source="[&lt;strong&gt;ExIsResourceAcquiredSharedLite&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredsharedlite)"><strong>ExIsResourceAcquiredSharedLite</strong></a> 例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxIsFcbAcquiredExclusive</strong> (<em>FCB</em>) </p></td>
<td align="left"><p>此宏检查当前线程是否有权访问独占模式下的常规资源。 此宏调用 <a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredexclusivelite" data-raw-source="[&lt;strong&gt;ExIsResourceAcquiredExclusiveLite&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredexclusivelite)"><strong>ExIsResourceAcquiredExclusiveLite</strong></a> 例程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxIsFcbAcquired</strong> (<em>FCB</em>) </p></td>
<td align="left"><p>此宏检查当前线程是否有权访问共享或独占模式下的常规资源。 此宏将调用 <a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredsharedlite" data-raw-source="[&lt;strong&gt;ExIsResourceAcquiredSharedLite&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredsharedlite)"><strong>ExIsResourceAcquiredSharedLite</strong></a> 和 <a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredexclusivelite" data-raw-source="[&lt;strong&gt;ExIsResourceAcquiredExclusiveLite&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-exisresourceacquiredexclusivelite)"><strong>ExIsResourceAcquiredExclusiveLite</strong></a> 例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxIsPrefixTableLockAcquired</strong> (<em>表</em>) </p></td>
<td align="left"><p>此宏指示在独占或共享模式下是否获取了前缀表锁。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxIsPrefixTableLockExclusive</strong> (<em>表</em>) </p></td>
<td align="left"><p>此宏指示是否以独占模式获取了前缀表锁。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxLog</strong> (<em>参数</em>) </p></td>
<td align="left"><p>在选中的生成上，此宏调用 <a href="/windows-hardware/drivers/ddi/rxlog/nf-rxlog-_rxlog" data-raw-source="[&lt;strong&gt;_RxLog&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxlog/nf-rxlog-_rxlog)"><strong>_RxLog</strong></a> 例程。</p>
<p>在零售版上，此宏不执行任何操作。</p>
<p>请注意， <strong>RxLog</strong> 的参数必须包含一对括号，以便在应关闭日志记录时允许转换为 null 调用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxLogEvent</strong> (<em>_DeviceObject</em>、 <em>_OriginatorId</em>、 <em>_EventId</em>、 <em>_Status</em>) </p></td>
<td align="left"><p>此宏调用 <a href="/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlogeventdirect" data-raw-source="[&lt;strong&gt;RxLogEventDirect&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlogeventdirect)"><strong>RxLogEventDirect</strong></a> 例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxLogFailure</strong> (<em>_DeviceObject</em>、 <em>_OriginatorId</em>、 <em>_EventId</em>、 <em>_Status</em>) </p></td>
<td align="left"><p>此宏调用 <a href="/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlogeventdirect" data-raw-source="[&lt;strong&gt;RxLogEventDirect&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlogeventdirect)"><strong>RxLogEventDirect</strong></a> 例程。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxLogFailureWithBuffer</strong> (<em>_DeviceObject</em>、 <em>_OriginatorId</em>、 <em>_EventId</em>、 <em>_Status</em>、 <em>_Buffer</em>_Length <em>) </em></p></td>
<td align="left"><p>此宏调用 <a href="/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlogeventwithbufferdirect" data-raw-source="[&lt;strong&gt;RxLogEventWithBufferDirect&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxprocs/nf-rxprocs-rxlogeventwithbufferdirect)"><strong>RxLogEventWithBufferDirect</strong></a> 例程。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxLogRetail</strong> (<em>参数</em>) </p></td>
<td align="left"><p>在选中的生成上，此宏调用 <a href="/windows-hardware/drivers/ddi/rxlog/nf-rxlog-_rxlog" data-raw-source="[&lt;strong&gt;_RxLog&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxlog/nf-rxlog-_rxlog)"><strong>_RxLog</strong></a> 例程。</p>
<p>在零售版上，此宏不执行任何操作。</p>
<p>请注意， <strong>RxLogRetail</strong> 的参数必须包含一对括号，以便在应关闭日志记录时允许转换为 null 调用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxReferenceNetFcb</strong> (<em>Fcb</em>) </p></td>
<td align="left"><p>此宏用于跟踪对 FCB 结构的引用操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxReferenceNetFobx</strong> (<em>Fobx</em>) </p></td>
<td align="left"><p>此宏用于跟踪对 FOBX 结构的引用操作。 日志记录系统和 WMI 可访问这些引用操作的日志。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxReferenceNetRoot</strong> (<em>NetRoot</em>) </p></td>
<td align="left"><p>此宏用于跟踪对 NET_ROOT 结构的引用操作。 日志记录系统可以访问这些引用操作的日志，并 Windows Management Instrumentation (WMI) 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxReferenceSrvCall</strong> (<em>SrvCall</em>) </p></td>
<td align="left"><p>此宏用于跟踪 (DPC) 级别未延迟的过程调用 SRV_CALL 结构的引用操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxReferenceSrvCallAtDpc</strong> (<em>SrvCall</em>) </p></td>
<td align="left"><p>此宏用于在 DPC 级别跟踪对 SRV_CALL 结构的引用操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxReferenceSrvOpen</strong> (<em>SrvOpen</em>) </p></td>
<td align="left"><p>此宏用于跟踪对 SRV_OPEN 结构的引用操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxReferenceVNetRoot</strong> (<em>VNetRoot</em>) </p></td>
<td align="left"><p>此宏用于跟踪对 V_NET_ROOT 结构的引用操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxReleasePrefixTableLock</strong> (<em>表</em>) </p></td>
<td align="left"><p>此宏释放前缀表锁。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>RxSynchronizeBlockingOperations</strong> (<em>RXCONTEXT</em>、<em>FCB</em>、<em>IOQUEUE</em>) </p></td>
<td align="left"><p>此宏将阻塞 i/o 请求同步到相同的工作队列。 在 Windows Server 2003 上，此宏调用 <a href="/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-__rxsynchronizeblockingoperations" data-raw-source="[&lt;strong&gt;__RxSynchronizeBlockingOperations&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-__rxsynchronizeblockingoperations)"><strong>__RxSynchronizeBlockingOperations</strong></a> 例程，并将 <em>DropFcbLock</em> 参数设置为 <strong>FALSE</strong>。</p>
<p>在 Windows XP 和 Windows 2000 上，此宏会调用 <a href="/windows-hardware/drivers/ifs/--rxsynchronizeblockingoperationsmaybedroppingfcblock" data-raw-source="[&lt;strong&gt;__RxSynchronizeBlockingOperationsMaybeDroppingFcbLock&lt;/strong&gt;](./--rxsynchronizeblockingoperationsmaybedroppingfcblock.md)"><strong>__RxSynchronizeBlockingOperationsMaybeDroppingFcbLock</strong></a> 例程，并将 <em>DropFcbLock</em> 参数设置为 <strong>FALSE</strong>。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>RxSynchronizeBlockingOperations</strong> (<em>RXCONTEXT</em>、<em>FCB</em>、<em>IOQUEUE</em>) </p></td>
<td align="left"><p>此宏将阻塞 i/o 请求同步到相同的工作队列。 在 Windows Server 2003 上，此宏调用 <a href="/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-__rxsynchronizeblockingoperations" data-raw-source="[&lt;strong&gt;__RxSynchronizeBlockingOperations&lt;/strong&gt;](/windows-hardware/drivers/ddi/rxcontx/nf-rxcontx-__rxsynchronizeblockingoperations)"><strong>__RxSynchronizeBlockingOperations</strong></a> 例程，并将 <em>DropFcbLock</em> 参数设置为 <strong>TRUE</strong>。</p>
<p>在 Windows XP 和 Windows 2000 上，此宏会调用 <a href="/windows-hardware/drivers/ifs/--rxsynchronizeblockingoperationsmaybedroppingfcblock" data-raw-source="[&lt;strong&gt;__RxSynchronizeBlockingOperationsMaybeDroppingFcbLock&lt;/strong&gt;](./--rxsynchronizeblockingoperationsmaybedroppingfcblock.md)"><strong>__RxSynchronizeBlockingOperationsMaybeDroppingFcbLock</strong></a> 例程，并将 <em>DropFcbLock</em> 参数设置为 <strong>TRUE</strong>。</p></td>
</tr>
</tbody>
</table>

 

