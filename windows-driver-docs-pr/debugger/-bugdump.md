---
title: bugdump
description: Bugdump 扩展会格式化并显示 bug 检查回调缓冲区中包含的信息。
keywords:
- bugdump Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- bugdump
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 958db9562672694a4538ecdb83d8a98d725e7fb9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814129"
---
# <a name="bugdump"></a>!bugdump


**！ Bugdump** extension 格式化并显示 bug 检查回调缓冲区中包含的信息。

```dbgsyntax
    !bugdump [Component] 
```

## <a name="span-idddk__bugdump_dbgspanspan-idddk__bugdump_dbgspanparameters"></a><span id="ddk__bugdump_dbg"></span><span id="DDK__BUGDUMP_DBG"></span>参数


<span id="_______Component______"></span><span id="_______component______"></span><span id="_______COMPONENT______"></span>*组件*   
指定要检查其回调数据的组件。 如果省略，则显示所有 bug 检查回调数据。

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

有关详细信息，请参阅 " [读取 Bug 检查回调数据](reading-bug-check-callback-data.md)"。

<a name="remarks"></a>备注
-------

此扩展只能在发生错误检查后，或在调试内核模式故障转储文件时使用。

*组件* 参数对应于 [**KeRegisterBugCheckCallback**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keregisterbugcheckcallback)中使用的最终参数。

保存回调数据的缓冲区在小型内存转储中不可用。 这些缓冲区存在于内核内存转储和完整内存转储中。 但是，在 Windows XP SP1、Windows Server 2003 和更高版本的 Windows 中，在调用驱动程序的 **BugCheckCallback** 例程之前会创建转储文件，因此这些缓冲区将不包含这些例程写入的数据。

如果要对崩溃的系统执行实时调试，则会显示所有回叫数据。

 

