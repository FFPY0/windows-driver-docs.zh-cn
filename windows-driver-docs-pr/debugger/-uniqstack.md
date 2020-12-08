---
title: uniqstack
description: Uniqstack 扩展显示当前进程中的所有线程的所有堆栈，排除似乎有重复项的堆栈。
keywords:
- uniqstack Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- uniqstack
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 284d5c0554d298a1aa7e46e9266ef41d621b5bfd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825271"
---
# <a name="uniqstack"></a>!uniqstack


**！ Uniqstack** 扩展显示当前进程中的所有线程的所有堆栈，排除似乎有重复项的堆栈。

```dbgcmd
!uniqstack [ -b | -v | -p ] [ -n ]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______-b______"></span><span id="_______-B______"></span>**-b**   
使显示包含传递给每个函数的前三个参数。

<span id="_______-v______"></span><span id="_______-V______"></span>**-v**   
使显示内容包括帧指针省略 (FPO) 信息。 在基于 x86 的处理器上，也会显示调用约定信息。

<span id="_______-p______"></span><span id="_______-P______"></span>**-p**   
使显示包含在堆栈跟踪中调用的每个函数的完整参数。 此列表将包括每个参数的数据类型、名称和值。 *这需要完整的符号信息。*

<span id="_______-n______"></span><span id="_______-N______"></span>**-n**   
导致显示帧号。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Uext.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Uext.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

此扩展类似于 [**k、kb、glm-kc-qnw、kd、kp、kp、kv (显示 Stack Backtrace)**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md) 命令，只不过它不显示重复堆栈。

例如：

```dbgcmd
0:000> !uniqstack
Processing 14 threads, please wait

.  0  Id: f0f0f0f0.15c Suspend: 1 Teb: 00000000`7fff8000 Unfrozen
      Priority: 0
Child-SP          Child-BSP         RetAddr
00000000`0006e5e0 00000000`00070420 00000000`6b009840
00000000`0006e600 00000000`000703d0 00000000`6b03db00
00000000`0006e950 00000000`000703b0 00000000`6b008520
00000000`0006e950 00000000`00070368 00000000`6b1845e0
00000000`0006e9b0 00000000`00070310 00000000`6b009980
00000000`0006e9d0 00000000`000702d0 00000000`6b009ff0
00000000`0006e9e0 00000000`00070248 00000000`77ea4a10
00000000`0006f290 00000000`000700e0 00000000`77ea5d60
00000000`0006f4c0 00000000`00070028 00000000`77ed6000
00000000`0006f550 00000000`00070000 00000000`77ed9000
00000000`0006f550 00000000`00070000 00000000`77ca78a0
00000000`0006fff0 00000000`00070000 00000000`00000000

.  1  Id: f0f0f0f0.718 Suspend: 1 Teb: 00000000`7fff4000 Unfrozen
      Priority: 0
Child-SP          Child-BSP         RetAddr
00000000`0043eb50 00000000`00440250 00000000`6b008520
00000000`0043eb80 00000000`00440208 00000000`6b1845e0
00000000`0043ebe0 00000000`004401a8 00000000`6b009980
00000000`0043ec00 00000000`00440168 00000000`6b009ff0
00000000`0043ec10 00000000`004400e0 00000000`77ea5f50
00000000`0043f4c0 00000000`00440028 00000000`77ed6000
00000000`0043f550 00000000`00440000 00000000`77ed9000
00000000`0043f550 00000000`00440000 00000000`7de05690
00000000`0043fff0 00000000`00440000 00000000`00000000

. 13  Id: f0f0f0f0.494 Suspend: 1 Teb: 00000000`7ef98000 Unfrozen
      Priority: 0
Child-SP          Child-BSP         RetAddr
00000000`00feffe0 00000000`00ff0040 00000000`77e94f30
00000000`00feffe0 00000000`00ff0040 00000000`00000000

Total threads: 14
Duplicate callstacks: 11 (windbg thread #s follow):
2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12
```

 

 





