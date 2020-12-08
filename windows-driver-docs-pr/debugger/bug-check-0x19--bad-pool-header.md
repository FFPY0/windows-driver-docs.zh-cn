---
title: Bug 检查 0x19 BAD_POOL_HEADER
description: BAD_POOL_HEADER bug 检查的值为0x00000019。 这表明池标头已损坏。
keywords:
- Bug 检查 0x19 BAD_POOL_HEADER
- BAD_POOL_HEADER
ms.date: 12/07/2017
topic_type:
- apiref
api_name:
- BAD_POOL_HEADER
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 06b5e9e9721bf6821adf5e990fc88cee2d46fac7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832003"
---
# <a name="bug-check-0x19-bad_pool_header"></a>Bug 检查0x19：错误的 \_ 池 \_ 标头

错误的 \_ 池 \_ 标头 bug 检查的值为0x00000019。 这表明池标头已损坏。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。

## <a name="bad_pool_header-parameters"></a>错误的 \_ 池 \_ 标头参数

参数1指示违规类型。 其他参数的意义取决于参数1的值。

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
<td align="left"><p>0x2</p></td>
<td align="left"><p>要检查的池条目</p></td>
<td align="left"><p>池块的大小</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>特殊池模式检查失败。</p>
<p> (所有者可能损坏了池块。 ) </p></td>
</tr>
<tr class="even">
<td align="left"><p>0x3</p></td>
<td align="left"><p>要检查的池条目</p></td>
<td align="left"><p>读回 <strong>flink</strong> freelist 值</p></td>
<td align="left"><p>读回 <strong>闪烁</strong> freelist 值</p></td>
<td align="left"><p>池 freelist 已损坏。</p>
<p> (在正常列表中，参数2、3和4的值应相同。 ) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x5</p></td>
<td align="left"><p>池条目之一</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>其他池条目</p></td>
<td align="left"><p>相邻池条目对具有彼此矛盾的标头。 其中至少有一个已损坏。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x6</p></td>
<td align="left"><p>一个错误计算条目</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>导致导致的错误项</p></td>
<td align="left"><p>池块标头的以前大小太大。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x7</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>错误池条目</p></td>
<td align="left"><p>池块标头大小已损坏。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x8</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>错误池条目</p></td>
<td align="left"><p>池块标头大小为零。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x9</p></td>
<td align="left"><p>一个错误计算条目</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>导致导致的错误项</p></td>
<td align="left"><p>池块标头大小已损坏 (它太大) 。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0xA</p></td>
<td align="left"><p>应找到的池条目</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>应该包含池条目的页面的虚拟地址</p></td>
<td align="left"><p>池块标头大小已损坏。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0xD、0xE、0xF、0x23、0x24、0x25</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>释放块后，已对其进行了修改。 这通常不是已释放的块的先前所有者的错误;它通常 (但并不总是) ，因为释放的块之前的块会溢出。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x20</p></td>
<td align="left"><p>应找到的池条目</p></td>
<td align="left"><p>下一个池条目</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>池块标头大小已损坏。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0X21</p></td>
<td align="left"><p>正在释放的池指针</p></td>
<td align="left"><p>为池块分配的字节数</p></td>
<td align="left"><p>池块后发现的损坏值</p></td>
<td align="left"><p>正在释放的池块后面的数据已损坏。 通常，这意味着使用者 (调用堆栈) 溢出了块。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0X22</p></td>
<td align="left"><p>正在释放的地址</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>正在释放的地址没有跟踪条目。 这通常是因为调用堆栈正在尝试释放已释放或从未分配给开头的指针。</p></td>
</tr>
</tbody>
</table>

<a name="cause"></a>原因
-----

池在当前请求时已损坏。

这可能是由调用方引起的，也可能不是。

<a name="resolution"></a>解决方法
----------

必须使用内核调试器遍历内部池链接，以找出问题的可能原因。

然后，可以将特殊池用于可疑池标记，或在可疑驱动程序上使用驱动程序验证程序 "特殊池" 选项。 在查明可疑驱动程序方面， [**！分析**](-analyze.md) 扩展可能会有所帮助，但池 corrupters 通常不会出现这种情况。

使用 [**蓝色屏幕数据**](blue-screen-data.md) 中所述的步骤来收集停止代码参数。 使用 stop 代码参数可确定正在跟踪的特定类型的代码行为。

**驱动程序验证程序**

驱动程序验证程序是一个实时运行的工具，用于检查驱动程序的行为。 如果发现驱动程序代码执行过程中出现错误，它会主动创建一个例外，以允许进一步审查驱动程序代码的一部分。 驱动程序验证程序管理器内置于 Windows 中，可在所有 Windows PC 上使用。 若要启动驱动程序验证程序管理器，请在命令提示下键入“验证程序”  。 你可以配置要验证的驱动程序。 验证驱动程序的代码在运行时会增加开销，因此请尝试验证尽可能少的驱动程序。 有关详细信息，请参阅[驱动程序验证程序](../devtest/driver-verifier.md)。

**Windows 内存诊断**

如果此错误检查显示不一致，则可能与错误的物理内存有关。

运行 Windows 内存诊断工具来测试内存。 在 "控制面板" 搜索框中键入 "内存"，然后选择 " **诊断计算机的内存问题**"。运行测试后，使用事件查看器查看系统日志下的结果。 查找“内存诊断结果”条目以查看结果  。
