---
title: 中断同步对象
description: 中断同步对象
keywords:
- helper 对象 WDK 音频，中断同步对象
- 中断同步对象 WDK 音频
- IInterruptSync 接口
- 同步 WDK 音频
- 中断服务例程 WDK 音频
- Isr WDK 音频
- 非中断例程 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e59efb92386d40043ac592d91c8391a437b56205
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784721"
---
# <a name="interrupt-sync-objects"></a>中断同步对象


## <span id="interrupt_sync_objects"></span><span id="INTERRUPT_SYNC_OBJECTS"></span>


PortCls 系统驱动程序实现 [IInterruptSync](/windows-hardware/drivers/ddi/portcls/nn-portcls-iinterruptsync) 接口，以获得微型端口驱动程序的优势。 **IInterruptSync** 表示一个中断同步对象，该对象将中断服务例程的列表执行与非中断例程同步 (isr) 。

中断同步对象提供两个主要功能：

-   执行 Isr 列表以响应中断。 同步对象连接到中断源。 每次发生中断时，sync 对象按照所选模式按指定顺序执行 Isr。  (查看三种模式的以下说明。 ) 

-   执行不 Isr 的例程。 这些非中断例程未连接到同步对象的中断。 相反，非中断例程会在调用方选择的时间运行。 但是，sync 对象会与对象的 Isr 列表同步执行非中断例程。 换句话说，非中断例程在同步对象列表中的任何 Isr 开始执行之前运行完毕，反之亦然。

中断同步对象对于处理多个 Isr 是灵活的。 Isr 驻留在同步对象在中断时进行遍历的链接列表中。 当微型端口驱动程序使用同步对象注册 ISR 时，它指定是否应将 ISR 添加到此列表的开头或结尾。

微型端口驱动程序调用 [**PcNewInterruptSync**](/windows-hardware/drivers/ddi/portcls/nf-portcls-pcnewinterruptsync) 函数来创建中断同步对象。 在此调用期间，驱动程序指定对象在中断时间遍历其 Isr 列表的方式。 此调用支持下表中的 INTERRUPTSYNCMODE 枚举常量指定的三个选项。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">返回的常量</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>InterruptSyncModeNormal</strong></p></td>
<td align="left"><p>调用列表中的每个 ISR，直到其中一个 ISR 返回 STATUS_SUCCESS。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>InterruptSyncModeAll</strong></p></td>
<td align="left"><p>无论前面 Isr 的返回代码如何，都只需调用列表中的每个 ISR 一次。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>InterruptSyncModeRepeat</strong></p></td>
<td align="left"><p>遍历整个 Isr 列表，直到列表中的任何 ISR 都返回 STATUS_SUCCESS。</p></td>
</tr>
</tbody>
</table>

 

在 **InterruptSyncModeNormal** 模式下，sync 对象将调用列表中的每个 ISR，直到其中一个 ISR 返回状态 " \_ 成功"。 此 ISR 后面的列表中的任何 Isr 都不会被调用。 此模式模拟操作系统通常处理 Isr 的方式。 如果 Isr 返回状态为 " \_ 成功"，则行为与 " **InterruptSyncModeAll**" 相同。

在 **InterruptSyncModeAll** 模式下，列表中的每个 ISR 只调用一次，而不考虑前面 isr 的返回代码。 这适用于更多的基元硬件，其中，中断的源是不确定的，尽管在其他情况下它可能也很有用。 例如，两个中断源可能会在每个中断上紧密同步，而不管特定中断来自哪个源。

在 **InterruptSyncModeRepeat** 模式下，sync 对象会反复遍历整个 isr 列表，直到到达列表中的任何例程返回状态 " \_ 成功"。 此模式适用于以下情况：来自多个源的中断可能会同时在同一中断线路上触发，或者在 ISR 处理期间可能会激发第二个中断。 每个中断源都必须能够确定是否需要处理。 如果始终返回状态 \_ "成功" 的 ISR 在此模式下注册到了同步对象，系统将停止响应。

在上述任何一种模式中，如果任何注册的 Isr 返回状态成功，则 sync 对象将向操作系统确认中断 \_ 。 在所有三种模式中，如果所有中断源指示它们未成功处理中断，则同步对象会将失败的结果代码返回给操作系统。

**IInterruptSync** 接口支持以下方法：

[**IInterruptSync::CallSynchronizedRoutine**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iinterruptsync-callsynchronizedroutine)

[**IInterruptSync：： Connect**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iinterruptsync-connect)

[**IInterruptSync：:D isconnect**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iinterruptsync-disconnect)

[**IInterruptSync::GetKInterrupt**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iinterruptsync-getkinterrupt)

[**IInterruptSync::RegisterServiceRoutine**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iinterruptsync-registerserviceroutine)

 

