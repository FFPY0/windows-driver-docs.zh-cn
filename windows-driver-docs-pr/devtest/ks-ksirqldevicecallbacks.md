---
title: 'KsIrqlDeviceCallbacks 规则 ( # A1'
description: KsIrqlDeviceCallbacks 规则指定内核流式处理 (KS) 微型端口驱动程序从带有调用时其具有相同 IRQL 的 KS 设备回调函数返回。
ms.date: 05/21/2018
keywords:
- 'KsIrqlDeviceCallbacks 规则 ( # A1'
topic_type:
- apiref
api_name:
- KsIrqlDeviceCallbacks
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 044d83ad33369e5cef26293f21a634a50b38b0ff
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811169"
---
# <a name="ksirqldevicecallbacks-rule-"></a>KsIrqlDeviceCallbacks 规则 ( # A1


KsIrqlDeviceCallbacks 规则指定内核流式处理 (KS) 微型端口驱动程序从带有调用时其具有相同 IRQL 的 KS 设备回调函数返回。

**调试提示**

当驱动程序验证器检测到与该规则的冲突时，它将触发 [**Bug 检查0xC4：驱动程序 \_ 验证程序 \_ 检测到 \_ 冲突**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md)， *arg1* 值为0x00081006。 Bug 检查的 *arg3* (RuleState) 和 *arg4*)  (子错误检查提供了指向有关规则冲突的其他信息的指针。

使用 [**！ ruleinfo**](../debugger/-ruleinfo.md) 调试器扩展来找出函数进入和退出时的 IRQL 值。

使用命令：

**！ ruleinfo 0x81006** *RuleState* 子 *情况。*

在规则状态数据中，输入回调时， *OldIrql* 是 IRQL。 退出回调函数时， *NewIrql* 是 IRQL。

不要使用 [**！ irql**](../debugger/-irql.md) 来确定当前的 irql，因为驱动程序验证程序可能在 bug 检查前引发了 irql。 改为使用 **！ verifier 0x008** 查看 IRQL 日志。

**驱动程序模型： KS**

**Bug 检查 () 发现此规则**： [**bug 检查0XC4：驱动程序 \_ 验证器 \_ 检测到 \_ 违反**](../debugger/bug-check-0xc4--driver-verifier-detected-violation.md) (0x00081006) 


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
<td align="left"><p>若要验证此规则，请打开 "命令提示符" 窗口。 输入 Driver Verifier 命令并指定 <strong>/domain ks</strong>。</p>
<p>例如：</p>
<p><strong>验证程序/domain ks</strong> [<em>options</em>] <strong>/driver</strong> <em> &lt; &gt; yourdriver</em></p>
<p>有关详细信息，请参阅<a href="/windows-hardware/drivers/devtest/driver-verifier" data-raw-source="[Driver Verifier](./driver-verifier.md)">驱动程序验证程序</a>。</p></td>
</tr>
</tbody>
</table>

 

