---
title: rpcexts.getcallinfo
description: Rpcexts getcallinfo 扩展在系统的 RPC 状态信息中搜索服务器端调用 (SCALL) 信息。
keywords:
- rpcexts getcallinfo Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- rpcexts.getcallinfo
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: fa2faa35812406f9dcfbd5455ed77fe19bc72b28
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838411"
---
# <a name="rpcextsgetcallinfo"></a>!rpcexts.getcallinfo


**！ Rpcexts getcallinfo** 扩展在系统的 RPC 状态信息中搜索服务器端调用 (SCALL) 信息。

```dbgcmd
!rpcexts.getcallinfo [ CallID | 0 [ IfStart | 0 [ ProcNum | 0xFFFF [ProcessID|0] ] ] ] 
!rpcexts.getcallinfo -? 
```

## <a name="span-idddk__rpcexts_getcallinfo_dbgspanspan-idddk__rpcexts_getcallinfo_dbgspanparameters"></a><span id="ddk__rpcexts_getcallinfo_dbg"></span><span id="DDK__RPCEXTS_GETCALLINFO_DBG"></span>参数


<span id="_______CallID______"></span><span id="_______callid______"></span><span id="_______CALLID______"></span>*CallID*   
指定呼叫 ID。 此参数是可选的;如果只想显示与特定 *CallID* 值匹配的调用，请将其包含在内。

<span id="_______IfStart______"></span><span id="_______ifstart______"></span><span id="_______IFSTART______"></span>*IfStart*   
指定在其上进行调用的接口 UUID 的第一个 DWORD。 此参数是可选的;如果只想显示与特定 *IfStart* 值匹配的调用，请将其包含在内。

<span id="_______ProcNum______"></span><span id="_______procnum______"></span><span id="_______PROCNUM______"></span>*ProcNum*   
指定此调用的过程号。 RPC Run-Time (RPC 通过 IDL 文件中的位置对其进行编号，来标识接口中的各个例程，接口中的第一个例程为0，第二个例程为1，依此类推。 ) 

<span id="_______ProcessID______"></span><span id="_______processid______"></span><span id="_______PROCESSID______"></span>*ProcessID*   
指定拥有要显示的调用的服务器进程 (PID) 的进程 ID。 此参数是可选的;如果要显示多个进程所拥有的调用，则省略它。

<span id="_______-_______"></span> **-?**   
在命令提示符窗口中显示此扩展的一些简短帮助文本。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>不可用</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Rpcexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关调试 Microsoft 远程过程调用 (RPC) 的详细信息，请参阅 [Rpc 调试](rpc-debugging.md)。

<a name="remarks"></a>备注
-------

此扩展只能与 CDB 一起使用，也可与用户模式 WinDbg 一起使用。

参数从左向右进行分析。 若要跳过某个参数，请提供值0。 此规则有一个例外：通过提供值0xFFFF，跳过 *ProcNum* 参数。

以下是示例：

```dbgcmd
0:002> !rpcexts.getcallinfo
Searching for call info ...
## PID  CELL ID   ST PNO IFSTART  TIDNUMBER CALLFLAG CALLID   LASTTIME CONN/CLN
----------------------------------------------------------------------------
00c4 0000.0006 00 009 367abb81 0000.0007 00000001 0000004a 00018b41 0000.0005
00c4 0000.000a 00 007 367abb81 0000.002d 00000001 0000009f 000134ff 0000.0009
00c4 0000.000d 00 00f 82273fdc 0000.002d 00000001 00000002 00036cd8 0000.0042
00c4 0000.0010 00 00f 367abb81 0000.002d 00000001 00000078 00011636 0000.000f
00c4 0000.0012 00 00d 8d9f4e40 0000.0007 00000001 0000004f 000097bd 0000.0011
00c4 0000.0015 00 000 367abb81 0000.0004 00000001 0000004c 0002cccf 0000.0014
00c4 0000.0017 00 007 367abb81 0000.0004 00000001 00000006 0000cf5e 0000.0016
00c4 0000.0018 00 000 367abb81 0000.002d 00000001 0000000b 0001236f 0000.002a
00c4 0000.0019 01 00b 82273fdc 0000.0002 00000009 00000000 00018b19 00d0.0104
00c4 0000.001b 00 009 65a93890 0000.0007 00000001 000000ea 0003cd14 0000.001a
00c4 0000.0021 00 03b 8d9f4e40 0000.0013 00000001 0000000b 0001162c 0000.0020
00c4 0000.0022 01 008 82273fdc 0000.001f 00000009 00000000 00013405 00c4.02e8
00c4 0000.0024 00 007 367abb81 0000.0004 00000001 00000006 0000f198 0000.0023
00c4 0000.0026 00 000 367abb81 0000.0036 00000001 000000ab 00038049 0000.0025
00c4 0000.0027 01 00b 82273fdc 0000.001f 00000009 00000000 00020b7c 00a8.0228
00c4 0000.0028 01 008 82273fdc 0000.003e 00000009 00000000 0003a949 0294.02f0
00c4 0000.0029 00 00d 8d9f4e40 0000.002d 00000001 0000033f 0003831a 0000.0031
00c4 0000.0030 00 03b 8d9f4e40 0000.0013 00000001 00000002 00024e43 0000.002f
00c4 0000.0032 01 008 82273fdc 0000.001f 00000009 00000000 000118f3 022c.019c
00c4 0000.0035 00 007 367abb81 0000.0033 00000001 00000074 0001042d 0000.0034
00c4 0000.0038 00 007 367abb81 0000.002d 00000001 0000000a 0002a3e4 0000.0037
00c4 0000.003a 00 007 367abb81 0000.0036 00000001 00000063 0003b7b8 0000.0039
00c4 0000.003b 00 004 3ba0ffc0 0000.002d 00000001 00000005 0002dd79 0000.002e
00c4 0000.003f 01 008 82273fdc 0000.0002 00000009 00000000 000245c6 01c0.037c
00c4 0000.0043 01 008 82273fdc 0000.0002 00000009 00000000 00037d50 020c.0394
00c4 0000.0049 00 008 8d9f4e40 0000.0007 00000001 000002b1 0004e900 0000.0048
0170 0000.0009 01 002 e60c73e6 0000.0002 00000009 baadf00d 0004ad30 020c.03a4
0170 0000.000a 01 002 0b0a6584 0000.0008 00000009 baadf00d 0001187b 00c4.012c
0170 0000.000c 01 002 0b0a6584 0000.0008 00000009 baadf00d 00011cdc 022c.019c
0170 0000.000d 01 003 00000136 0000.0011 00000009 baadf00d 00034845 020c.02b4
0170 0000.000e 01 000 412f241e 0000.0002 00000009 baadf00d 00012491 0294.02b8
0170 0000.000f 01 002 0b0a6584 0000.0011 00000009 baadf00d 000492e7 026c.0118
0170 0000.0010 01 002 e60c73e6 0000.0013 00000009 baadf00d 0004ab78 0378.038c
0170 0000.0014 01 004 e60c73e6 0000.0011 00000001 baadf00d 0002bc25 0378.024c
0170 0000.0015 01 003 00000136 0000.0013 00000009 00000003 00031d8d 0378.00b8
0170 0000.0018 01 004 00000136 0000.0002 00000001 baadf00d 00032e05 020c.026c
020c 0000.0004 01 003 00000132 0000.000b 00000009 00000000 00034953 0170.0240
020c 0000.000e 01 001 2f5f6520 0000.001e 00000009 00120006 00035bac 020c.03b4
020c 0000.0010 01 000 629b9f66 0000.000f 00000009 00000000 000279ff 00a8.0194
020c 0000.0011 01 004 faedcf59 0000.0003 00000009 00000012 0003836b 0378.024c
020c 0000.0012 01 001 629b9f66 0000.000f 00000009 00000000 0003657e 020c.02ec
020c 0000.0017 01 005 00000134 0000.0002 00000001 00000016 0003836b 0378.024c
020c 0000.001d 01 001 2f5f6520 0000.0014 00000001 0020007d 000351b2 020c.0258
0294 0000.0004 01 004 00000132 0000.0002 00000009 00000000 0003b786 0170.01ac
0378 0000.0004 01 003 00000134 0000.0003 0000000b 00300038 0002d896 020c.021c
026c 0000.0004 02 000 19bb5061 0000.0002 00000001 00000001 0004caa5 0000.0003
```

有关使用 DbgRpc 工具的类似示例，请参阅 [获取 RPC 调用信息](get-rpc-call-information.md)。

 

 





