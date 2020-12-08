---
title: 其他数据空间
description: 其他数据空间
keywords:
- 调试器引擎 API，内存，数据空间
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: dd8639eb576275f81920407b9e1d0cbc6340b515
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788771"
---
# <a name="other-data-spaces"></a>其他数据空间


## <span id="ddk_other_data_spaces_dbx"></span><span id="DDK_OTHER_DATA_SPACES_DBX"></span>


在内核模式调试中，除了主内存和寄存器外，还可以读取数据并将数据写入到各种数据空间。 可以访问以下数据空间：

<span id="System_Bus"></span><span id="system_bus"></span><span id="SYSTEM_BUS"></span>系统总线  
[**ReadBusData**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-readbusdata)和 [**WriteBusData**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-writebusdata)方法用于读取和写入系统总线数据。

<span id="Control-Space_Memory"></span><span id="control-space_memory"></span><span id="CONTROL-SPACE_MEMORY"></span>控制空间内存  
方法 [**ReadControl**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-readcontrol) 和 [**WriteControl**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-writecontrol) 读取和写入控制空间内存。

<span id="i_o_memory."></span><span id="I_O_MEMORY."></span>I/o 内存。  
方法 [**ReadIo**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-readio) 和 [**WriteIo**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-writeio) 读取和写入系统和总线 i/o 内存。

<span id="Model_Specific_Register__MSR_"></span><span id="model_specific_register__msr_"></span><span id="MODEL_SPECIFIC_REGISTER__MSR_"></span> (MSR) 的模型特定寄存器  
方法 [**ReadMsr**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-readmsr) 和 [**WriteMsr**](/windows-hardware/drivers/ddi/wdbgexts/nf-wdbgexts-writemsr) 读取和写入 MSRs，这是为特定 CPU 型号启用和禁用功能并支持调试的控制寄存器。

### <a name="span-idhandlesspanspan-idhandlesspan-handles"></a><span id="handles"></span><span id="HANDLES"></span> 手柄

在用户模式调试中，可以使用目标进程所拥有的系统句柄来获取有关系统对象的信息。 方法 [**ReadHandleData**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugdataspaces4-readhandledata) 可用于读取此信息。

可以通过使用 [**GetCurrentThreadHandle**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects4-getcurrentthreadhandle) 和 [**GetCurrentProcessHandle**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugsystemobjects-getcurrentprocesshandle) 方法获取线程和进程系统对象的系统句柄。 当创建线程和进程调试事件发生时，还将这些句柄提供给 [**IDebugEventCallbacks：： CreateThread**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugeventcallbacks-createthread) 和 [**IDebugEventCallbacks：： CreateProcess**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugeventcallbacks-createprocess) 回调方法。

**注意**   在内核模式下，进程和线程句柄是人工句柄。 它们不是系统句柄。

 

 

