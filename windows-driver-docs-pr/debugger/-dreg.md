---
title: dreg
description: Dreg 扩展显示注册表信息。
keywords:
- dreg Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dreg
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e91e98b71471899c13be089289c4164c1ec3acb2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816441"
---
# <a name="dreg"></a>!dreg


**！ Dreg** extension 显示注册表信息。

```dbgcmd
!dreg [-d|-w] KeyPath[!Value] 
!dreg
```

## <a name="span-idddk__dreg_dbgspanspan-idddk__dreg_dbgspanparameters"></a><span id="ddk__dreg_dbg"></span><span id="DDK__DREG_DBG"></span>参数


<span id="_______-d______"></span><span id="_______-D______"></span>**-d**   
导致二进制值显示为 Dword 值。

<span id="_______-w______"></span><span id="_______-W______"></span>**-w**   
导致二进制值显示为单词。

<span id="_______KeyPath______"></span><span id="_______keypath______"></span><span id="_______KEYPATH______"></span>*KeyPath*   
指定注册表项路径。 它可以以以下任何缩写开头：

<span id="hklm"></span><span id="HKLM"></span>**hklm**  
HKEY \_ 本地 \_ 计算机

<span id="hkcu"></span><span id="HKCU"></span>**hkcu**  
HKEY \_ 当前 \_ 用户

<span id="hkcr"></span><span id="HKCR"></span>**hkcr**  
HKEY \_ 类 \_ 根

<span id="hku"></span><span id="HKU"></span>**hku 开头**  
HKEY \_ 用户

如果未使用缩写， \_ \_ 则假定 HKEY 本地计算机。

<span id="_______Value______"></span><span id="_______value______"></span><span id="_______VALUE______"></span>*值*   
指定要显示的注册表值的名称。 如果使用星号 (\*) ，则显示所有值。 如果省略 *值* ，则显示所有子项。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>Ntsdexts.dll</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Ntsdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关注册表的信息，请参阅 Windows 驱动程序工具包 (WDK) 文档和 *Microsoft Windows 内部机制* ，Mark Russinovich 和 David 所罗门群岛。

<a name="remarks"></a>备注
-------

**！ Dreg** 扩展可用于在用户模式调试过程中显示注册表。

在远程调试过程中，它最有用，因为这样可以浏览远程计算机的注册表。 在从内核调试器控制用户模式调试器时，这一点也很有用，因为在目标计算机被冻结时无法在目标计算机上运行标准注册表编辑器。  (也可以为此目的使用 [**sleep**](-sleep--pause-debugger-.md) 命令。 有关详细信息，请参阅 [控制内核调试器中的 User-Mode 调试程序](controlling-the-user-mode-debugger-from-the-kernel-debugger.md) ) 

在本地调试时，它也很有用，因为信息是以一种易于阅读的格式呈现的。

如果在内核模式调试过程中使用 **！ dreg** ，则显示的结果将适用于主计算机而不是目标计算机。 若要显示目标计算机的原始注册表信息，请改用 [**！ reg**](-reg.md) 扩展。

下面是一些示例。 以下内容将显示指定注册表项的所有子项：

```dbgcmd
!dreg hkcu\Software\Microsoft
```

以下内容将显示指定注册表项中的所有值：

```dbgcmd
!dreg System\CurrentControlSet\Services\Tcpip!*
```

以下内容将在指定的注册表项中显示值开始：

```dbgcmd
!dreg System\CurrentControlSet\Services\Tcpip!Start
```

键入 **！** 不带任何参数的 dreg 将在调试器命令窗口中显示此扩展的一些简短帮助文本。

 

 





