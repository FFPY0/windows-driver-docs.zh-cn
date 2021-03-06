---
title: .scriptlist（列出已加载的脚本）
description: Scriptlist 命令列出加载的脚本。
keywords:
- scriptlist (列出) Windows 调试的已加载脚本
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- .scriptlist (List Loaded Scripts)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8e30392ef0c2209040b8b0e7427e561fa6b72c13
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805783"
---
# <a name="scriptlist-list-loaded-scripts"></a>.scriptlist（列出已加载的脚本）


**Scriptlist** 命令列出加载的脚本。

```dbgcmd
.scriptlist 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______________"></span>    
无

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>用户模式，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>all</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

Scriptlist 命令将列出已通过. scriptload 命令加载的任何脚本。

如果使用 scriptload 成功加载了 TestScript，则 scriptlist 命令会显示加载的脚本的名称。

```dbgcmd
0:000> .scriptlist
Command Loaded Scripts:
    JavaScript script from 'C:\WinDbg\Scripts\TestScript.js'
```

**惠?**

使用任何脚本命令之前，需要加载脚本提供程序。 使用 [**load (负载扩展 DLL)**](-load---loadby--load-extension-dll-.md) 命令加载 JavaScript 提供程序。

```dbgcmd
0:000> .load jsprovider.dll
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[JavaScript 调试器脚本](javascript-debugger-scripting.md)

[**.scriptload（加载脚本）**](-scriptload--load-script-.md)

 

 






