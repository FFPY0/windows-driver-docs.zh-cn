---
title: 日志记录和调查
description: 本主题介绍 GPIO 实现的日志记录和调查。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: fbddf175c1509ef34e6199f0aacc4fd498e18235
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830595"
---
# <a name="logging-and-investigations"></a>日志记录和调查


本主题介绍 GPIO 实现的日志记录和调查。

## <a name="span-idlive_debug_prints_from_the_kernel_debuggerspanspan-idlive_debug_prints_from_the_kernel_debuggerspanspan-idlive_debug_prints_from_the_kernel_debuggerspanlive-debug-prints-from-the-kernel-debugger"></a><span id="Live_debug_prints_from_the_kernel_debugger"></span><span id="live_debug_prints_from_the_kernel_debugger"></span><span id="LIVE_DEBUG_PRINTS_FROM_THE_KERNEL_DEBUGGER"></span>从内核调试器打印实时调试


``` syntax
!wmitrace.start buttonTrace -kd ; !wmitrace.enable buttonTrace {5a81715a-84c0-4def-ae38-edde40df5b3a} -level 4 -flag 0xFFFFFFFF
<repro>
!wmitrace.stop buttonTrace
```

## <a name="span-idlogs_and_investigationsspanspan-idlogs_and_investigationsspanspan-idlogs_and_investigationsspanlogs-and-investigations"></a><span id="Logs_and_investigations"></span><span id="logs_and_investigations"></span><span id="LOGS_AND_INVESTIGATIONS"></span>日志和调查


KD 中的 IFR 日志：

``` syntax
!rcdrkd msgpiowin32 
```

LogMan

``` syntax
 
logman start -ets buttonTrace -p {5a81715a-84c0-4def-ae38-edde40df5b3a} 0xFFFFFFFF 4
<repro>
logman stop -ets buttonTrace
```

### <a name="span-idvalidationsspanspan-idvalidationsspanspan-idvalidationsspanvalidations"></a><span id="Validations"></span><span id="validations"></span><span id="VALIDATIONS"></span>验证

你可以使用 IFR 日志或 Logman 来验证状态是否正确切换。

例如，如果需要更改插接指示器，则应在触发通知时在日志中找到以下条目。

``` syntax
--- start of log ---
10: Indicator_EvtDevicePrepareHardware - Received 0 resource descriptors, assuming indicator status will be injected via WriteFile
11: Indicator_EvtIoWrite - Indicator state change : DockMode_Indicator : old state : NotDocked
12: Indicator_UpdateRegistryValue - Indicator state update : DockMode_Indicator : new state : Docked
```

 

 




