---
title: pcr
description: Pcr 扩展显示特定处理器 (PCR) 的处理器控制区域的当前状态。
keywords:
- )  (的 PCR 的处理器控制区域
- pcr Windows 调试
ms.date: 10/07/2019
topic_type:
- apiref
api_name:
- pcr
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ad3414e989e2e14d9d6f29eb887cf4aa570d7dac
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837829"
---
# <a name="pcr"></a>!pcr


**！ Pcr** 扩展显示特定处理器 (pcr) 的处理器控制区域的当前状态。

```dbgcmd
!pcr [Processor]
```

## <a name="span-idddk__pcr_dbgspanspan-idddk__pcr_dbgspanparameters"></a><span id="ddk__pcr_dbg"></span><span id="DDK__PCR_DBG"></span>参数


<span id="_______Processor______"></span><span id="_______processor______"></span><span id="_______PROCESSOR______"></span>*处理器*   
指定要从中检索 PCR 信息的处理器。 如果省略了 *processor* ，则使用当前处理器。

> [!NOTE]
> 此命令目前不受支持，可能会显示不正确的输出。
>

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Kdextx86.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>



### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关 PCR 和 PRCB 的信息，请参阅 *Microsoft Windows 内部机制*，标记为 Russinovich 和 David 所罗门群岛。

<a name="remarks"></a>备注
-------

处理器控制块 (PRCB) 为 PCR 的扩展。 它可以与 [**！ prcb**](-prcb.md) 扩展名一起显示。

以下是 x86 目标计算机上的 " **！ pcr** " 扩展的示例：

```dbgcmd
kd> !pcr 0
KPCR for Processor 0 at ffdff000:
    Major 1 Minor 1
      NtTib.ExceptionList: 801626e0
          NtTib.StackBase: 801628f0
         NtTib.StackLimit: 8015fb00
       NtTib.SubSystemTib: 00000000
            NtTib.Version: 00000000
        NtTib.UserPointer: 00000000
            NtTib.SelfTib: 00000000

                  SelfPcr: ffdff000
                     Prcb: ffdff120
                     Irql: 00000000
                      IRR: 00000000
                      IDR: ffffffff
            InterruptMode: 00000000
                      IDT: 80043400
                      GDT: 80043000
                      TSS: 803cc000

            CurrentThread: 8015e8a0
               NextThread: 00000000
               IdleThread: 8015e8a0

                DpcQueue:  0x80168ee0 0x80100d04 ntoskrnl!KiTimerExpiration
```

此显示中的其中一项显示中断请求级别 (IRQL) 。 **！ Pcr** 扩展显示当前的 irql，但当前的 irql 通常不太重要。 与 bug 检查或调试器连接相同的 IRQL 更有趣。 这由 [**！ irql**](-irql.md)显示，后者仅在运行 windows Server 2003 或更高版本的 windows 的计算机上可用。









