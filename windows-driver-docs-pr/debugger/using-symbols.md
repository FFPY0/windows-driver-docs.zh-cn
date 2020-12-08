---
title: 使用符号
description: 使用符号
keywords:
- 调试器引擎，符号
- symbols
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 62daa89325d29bf1584d1332613eeb9bcc674f78
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803063"
---
# <a name="using-symbols"></a>使用符号


## <span id="ddk_symbols_dbx"></span><span id="DDK_SYMBOLS_DBX"></span>


有关符号（包括使用符号文件和符号服务器）的概述，请参见 [符号](symbols.md)。

### <a name="span-idsymbol_names_and_locationsspanspan-idsymbol_names_and_locationsspansymbol-names-and-locations"></a><span id="symbol_names_and_locations"></span><span id="SYMBOL_NAMES_AND_LOCATIONS"></span>符号名称和位置

若要查找符号名称，请使用 [**GetOffsetByName**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getoffsetbyname)。 有关用于指定符号名称的语法的详细信息，请参阅 [符号语法和符号匹配](symbol-syntax-and-symbol-matching.md)。

如果符号的准确名称未知，或多个符号具有相同的名称，则 [**StartSymbolMatch**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-startsymbolmatch) 将开始搜索名称与给定模式匹配的符号。 有关语法的详细信息，请参阅 [字符串通配符语法](string-wildcard-syntax.md)。

若要在给定位置的位置查找符号名称，请使用 [**GetNameByOffset**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getnamebyoffset)。 若要在给定位置附近的模块中查找符号名称，请使用 [**GetNearNamebyOffset**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getnearnamebyoffset)。

**注意**   请尽可能用模块名称（例如 **mymodule！ main**）限定符号。 否则，如果符号不存在 (例如，由于键入错误) ，引擎将必须为每个模块加载和搜索符号;这可能是一个慢速进程，特别是对于内核模式调试。 如果使用模块名称限定符号名称，则引擎只需搜索该模块的符号。

 

使用 "结构" [**调试 \_ 模块 \_ 和 \_ ID**](/windows-hardware/drivers/ddi/dbgeng/ns-dbgeng-_debug_module_and_id)唯一标识符号。 此结构由 [**GetSymbolEntriesByName**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getsymbolentriesbyname) 和 [**GetSymbolEntriesByOffset**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getsymbolentriesbyoffset)方法返回，后者分别基于其名称和位置搜索符号。

方法 [**GetSymbolEntryInformation**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getsymbolentryinformation) 使用 [**调试 \_ 符号 \_ 条目**](/windows-hardware/drivers/ddi/dbgeng/ns-dbgeng-_debug_symbol_entry) 结构返回符号说明。

若要查找结构内字段的偏移量，请使用 [**GetFieldOffset**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols-getfieldoffset)。 若要查找字段在结构中给定索引的名称，请使用 [**GetFieldName**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getfieldname)。 若要查找枚举常量的值，请使用 [**GetConstantName**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getconstantname)。

方法 [**GetSymbolInformation**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugadvanced3-getsymbolinformation) 可以执行多个有关符号信息的请求。

### <a name="span-idsymbol_optionsspanspan-idsymbol_optionsspansymbol-options"></a><span id="symbol_options"></span><span id="SYMBOL_OPTIONS"></span>符号选项

许多选项控制如何加载和卸载符号。 有关这些选项的说明，请参阅 [设置符号选项](symbol-options.md)。

可以使用 [**AddSymbolOptions**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-addsymboloptions)打开符号选项，并通过使用 [**RemoveSymbolOptions**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-removesymboloptions)将其关闭。

[**GetSymbolOptions**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getsymboloptions) 返回当前符号选项。 若要同时设置所有符号选项，请使用 [**SetSymbolOptions**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-setsymboloptions)。

### <a name="span-idreloading_symbolsspanspan-idreloading_symbolsspanreloading-symbols"></a><span id="reloading_symbols"></span><span id="RELOADING_SYMBOLS"></span>重新加载符号

加载符号文件后，引擎会将符号信息存储在内部缓存中。 若要刷新此缓存，请使用 [**重载**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-reload)。 现在，必须重新加载这些符号或以后再加载。

### <a name="span-idsynthetic_symbolsspanspan-idsynthetic_symbolsspan-synthetic-symbols"></a><span id="synthetic_symbols"></span><span id="SYNTHETIC_SYMBOLS"></span> 综合符号

*综合符号* 是用于标记任意地址以便于引用的一种方法。 可以在任何现有模块中创建综合符号。 方法 [**AddSyntheticSymbol**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-addsyntheticsymbol) 创建新的合成符号。 可以使用 [**RemoveSyntheticSymbol**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-removesyntheticsymbol)删除综合符号。 重新加载模块的符号将删除与该模块关联的所有合成符号。

### <a name="span-idsymbol_pathspanspan-idsymbol_pathspansymbol-path"></a><span id="symbol_path"></span><span id="SYMBOL_PATH"></span>符号路径

若要将目录或符号服务器添加到符号路径中，请使用方法 [**AppendSymbolPath**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-appendsymbolpath)。 整个符号路径由 [**GetSymbolPath**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-getsymbolpath) 返回，可使用 [**SetSymbolPath**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsymbols3-setsymbolpath)进行更改。

 

