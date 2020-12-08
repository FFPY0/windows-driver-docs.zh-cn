---
title: dds、dps、dqs（显示单词和符号）
description: Dds、dps 和 dqs 命令显示给定范围内内存的内容。 此内存假定为符号表中的一系列地址。
keywords:
- dds、dps、dqs (显示) Windows 调试的单词和符号
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- dds, dps, dqs (Display Words and Symbols)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 453e6979e9ea8ed9788a15cb0111866d8b8aa0e4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823447"
---
# <a name="dds-dps-dqs-display-words-and-symbols"></a>dds、dps、dqs（显示单词和符号）


**Dds**、 **dps** 和 **dqs** 命令显示给定范围内内存的内容。 此内存假定为符号表中的一系列地址。 还显示相应的符号。

```dbgcmd
dds [Options] [Range] 
dqs [Options] [Range] 
dps [Options] [Range] 
```

## <a name="span-idddk_cmd_display_words_and_symbols_dbgspanspan-idddk_cmd_display_words_and_symbols_dbgspanparameters"></a><span id="ddk_cmd_display_words_and_symbols_dbg"></span><span id="DDK_CMD_DISPLAY_WORDS_AND_SYMBOLS_DBG"></span>参数


<span id="_______Options______"></span><span id="_______options______"></span><span id="_______OPTIONS______"></span>*选项*   
指定一个或多个显示选项。 可以包含以下任何选项，但不能指定多个 **/p** \* 选项：

<span id="_c_Width"></span><span id="_c_width"></span><span id="_C_WIDTH"></span>**/c** *Width*  
指定要在显示中使用的列数。 如果省略此值，则默认的列数取决于显示类型。 由于这些命令显示符号的方式，通常最好只使用一个数据列的默认值。

<span id="_p"></span><span id="_P"></span>**/p**  
仅 (内核模式) 使用物理内存地址进行显示。 *范围* 指定的范围将从物理内存而不是虚拟内存中获取。

<span id="_p_c_"></span><span id="_P_C_"></span>**/p \[ c\]**  
 (内核模式仅) 与 **/P** 相同，不同之处在于缓存的内存将被读取。 必须包括 **c** 的方括号。

<span id="_p_uc_"></span><span id="_P_UC_"></span>**/p \[ uc\]**  
 (内核模式仅) 与 **/P** 相同，不同之处在于将读取未缓存的内存。 必须包括 **uc** 周围的方括号。

<span id="_p_wc_"></span><span id="_P_WC_"></span>**/p \[ wc.exe\]**  
 (内核模式仅) 与 **/P** 相同，不同之处在于将读取写入合并内存。 必须包含 **wc.exe** 两侧的方括号。

<span id="_______Range______"></span><span id="_______range______"></span><span id="_______RANGE______"></span>*范围*   
指定要显示的内存区域。 有关更多语法详细信息，请参阅 [地址和地址范围语法](address-and-address-range-syntax.md)。 如果省略 *Range*，则该命令将显示从上一个显示命令的结束位置开始的内存。 如果省略 *Range* 并且未使用上一个显示命令，则显示从当前指令指针开始。 如果提供了简单地址，则默认范围长度为128字节。

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

**模式**：用户模式，内核模式

**目标**：实时、崩溃转储

**平台**：所有

 

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关内存操作的概述以及其他与内存相关的命令的说明，请参阅 [读取和写入内存](reading-and-writing-memory.md)。

<a name="remarks"></a>备注
-------

**Dds** 的第二个字符区分大小写。 所有这些命令的第三个字符区分大小写。

**Dds** 命令显示双引号 (4 个字节) 值，例如 [**dd**](d--da--db--dc--dd--dd--df--dp--dq--du--dw--dw--dyb--dyd--display-memor.md)命令。 **Dqs** 命令显示四字 (8 字节) 值，例如 **dq** 命令。 **Dps** 命令 (4 字节或8字节显示指针大小的值，具体取决于目标计算机的体系结构) 类似于 **dp** 命令。

其中的每个词都被视为符号表中的地址。 为每个单词显示相应的符号信息。

如果已启用行号信息，将显示源文件名和行号（如果可用）。

 

 





