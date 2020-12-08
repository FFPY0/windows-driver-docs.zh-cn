---
title: ndiskd.dbglevel
description: Ndiskd dbglevel 扩展显示，并根据需要更改当前的 NDIS 调试级别。 警告 ndiskd 已被 WPP 和驱动程序验证程序取代。
keywords:
- ndiskd dbglevel Windows 调试
ms.date: 06/15/2020
topic_type:
- apiref
api_name:
- ndiskd.dbglevel
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 24757120800234f3f6b49c9b1034f99c9232bb2e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796335"
---
# <a name="ndiskddbglevel"></a>!ndiskd.dbglevel

**！ Ndiskd dbglevel** 扩展显示，并根据需要更改当前的 NDIS 调试级别。

**警告**  
**！ ndiskd** 已被 WPP (Windows 软件跟踪预处理器) 和驱动程序验证程序所取代。 ！如果目标系统不支持 **！ ndiskd dbglevel**，ndiskd 将为你提供以下警告。

```console
0: kd> !ndiskd.dbglevel
    This target does not support tracing through !ndiskd.dbglevel or
    !ndiskd.dbgsystems.
    Learn how to collect traces with WPP
```

如果单击警告底部的链接，！ ndiskd 将会获得详细信息。

```console
0: kd> !ndiskd.help wpptracing
    WPP traces are fast, flexible, and detailed.  Plus, starting with Windows 8
    and Windows Server 2012, you can automatically decode NDIS traces using the
    symbol file.  Just point TraceView (or tracepdb.exe) at NDIS.PDB, and it
    will be able to get all the TMFs it needs to trace NDIS activity.
    
    If you would like traces to be printed in the debugger window, you use the
    !wmitrace extension.  For example, you might enable traces with this:

    !wmitrace.searchpath c:\path\to\TMF\files
    !wmitrace.start ndis -kd
    !wmitrace.enable ndis {DD7A21E6-A651-46D4-B7C2-66543067B869} -level 4 -flag 0x31f3
```

有关 WPP 的详细信息，请参阅 [Wpp 软件跟踪](../devtest/wpp-software-tracing.md)。

有关驱动程序验证程序的详细信息，请参阅 [驱动程序验证](../devtest/driver-verifier.md)器。

有关 WMI 跟踪的详细信息，请参阅 [Wmi 跟踪扩展 ( # A0) ](wmi-tracing-extensions--wmitrace-dll-.md)。

```console
!ndiskd.dbglevel [-level <str>]
```

## <a name="parameters"></a>参数

<span id="_______-level______"></span><span id="_______-LEVEL______"></span>*-级别*   
调试详细级别。 可能的值为：

- 无-禁用调试跟踪
- 严重-启用要打印的致命错误
- 错误-启用打印错误
- 警告-启用要打印的警告
- INFO-启用要打印的信息性消息
- 详细-启用要打印的所有调试跟踪

### <a name="dll"></a>DLL

Ndiskd.dll

### <a name="remarks"></a>备注

此扩展仅适用于选中 NDIS.sys。 若要检查 NDIS.sys 的生成信息，请运行 [**！ ndiskd**](-ndiskd-ndis.md) 扩展名。

## <a name="see-also"></a>请参阅

[网络驱动程序设计指南](../network/index.md)

[Windows Vista 和更高版本的网络引用](/windows-hardware/drivers/ddi/_netvista/)

[调试网络堆栈](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 扩展 ( # A0)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[**!ndiskd.ndis**](-ndiskd-ndis.md)

[WPP 软件跟踪](../devtest/wpp-software-tracing.md)

[驱动程序验证程序](../devtest/driver-verifier.md)

[WMI 跟踪扩展 (Wmitrace.dll)](wmi-tracing-extensions--wmitrace-dll-.md)
