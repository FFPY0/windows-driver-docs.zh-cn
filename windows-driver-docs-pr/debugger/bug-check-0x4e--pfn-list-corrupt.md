---
title: Bug 检查 0x4E PFN_LIST_CORRUPT
description: PFN_LIST_CORRUPT bug 检查的值为0x0000004E。 这表明) 列表 (PFN 的页面帧号。
keywords:
- Bug 检查 0x4E PFN_LIST_CORRUPT
- PFN_LIST_CORRUPT
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- PFN_LIST_CORRUPT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4526f61c168d5884417556bb74ab7e7ce03ab875
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831629"
---
# <a name="bug-check-0x4e-pfn_list_corrupt"></a>Bug 检查0x4E： PFN \_ 列表 \_ 已损坏


PFN \_ LIST \_ 损坏 bug 检查的值为0x0000004E。 这表明) 列表 (PFN 的页面帧号。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="pfn_list_corrupt-parameters"></a>PFN \_ 列出 \_ 损坏的参数


*参数 1* 指示违规类型。 其他参数的意义取决于 *参数 1* 的值。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数 1</th>
<th align="left">参数2</th>
<th align="left">参数3</th>
<th align="left">参数4</th>
<th align="left">错误的原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x01</p></td>
<td align="left"><p>已损坏的 <strong>ListHead</strong> 值</p></td>
<td align="left"><p>可用页数</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>列表头已损坏。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x02</p></td>
<td align="left"><p>列表中要删除的项</p></td>
<td align="left"><p>最高物理页码</p></td>
<td align="left"><p>要删除的项的引用计数</p></td>
<td align="left"><p>列表项已损坏。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x07</p></td>
<td align="left"><p>页面框架编号</p></td>
<td align="left"><p>当前共享计数</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>驱动程序已解锁某个页面的次数超过其锁定时间。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x8D</p></td>
<td align="left"><p>状态不一致的页面框架编号</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>无页列表已损坏。 此错误代码很可能指示出现硬件问题。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x8F</p></td>
<td align="left"><p>新页码</p></td>
<td align="left"><p>旧页码</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>免费或零的页 listhead 已损坏。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x99</p></td>
<td align="left"><p>页面框架编号</p></td>
<td align="left"><p>当前页面状态</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p> (PTE) 或 PFN 的页表项已损坏。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x9A</p></td>
<td align="left"><p>页面框架编号</p></td>
<td align="left"><p>当前页面状态</p></td>
<td align="left"><p>要删除的项的引用计数</p></td>
<td align="left"><p>驱动程序尝试释放对 IO 仍处于锁定状态的页。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

此错误通常是由驱动程序传递错误的内存描述符列表导致的。 例如，驱动程序可能使用同一列表调用了两次 **MmUnlockPages** 。

如果内核调试器可用，请检查堆栈跟踪： [**！分析**](-analyze.md) 调试扩展显示有关 bug 检查的信息，可帮助确定根本原因，然后输入一个 [**k (显示堆栈 Backtrace)**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md) 命令来查看调用堆栈。

 

 




