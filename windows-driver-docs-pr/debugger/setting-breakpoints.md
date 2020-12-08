---
title: 设置断点
description: 设置断点
keywords:
- 调试器引擎 API，设置断点
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: e836d0efaf93ce4cc79caf6c32f7a36a7d3700bf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840201"
---
# <a name="setting-breakpoints"></a>设置断点


## <span id="ddk_using_breakpoints_dbx"></span><span id="DDK_USING_BREAKPOINTS_DBX"></span>


断点是通过 [**AddBreakpoint**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-addbreakpoint) 方法创建的。 此方法创建一个 [IDebugBreakpoint](/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugbreakpoint) 对象，该对象表示断点。 它还 (软件断点或处理器断点) 设置 *断点类型* 。 创建断点后，将无法更改其类型。

通过 [**了 removebreakpoint 时**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-removebreakpoint) 方法删除断点。 此操作还会删除 **IDebugBreakpoint** 对象;此对象不能再次使用。

**注意**   尽管 **IDebugBreakpoint** 实现 **iunknown** 接口，但不使用方法 **IUnknown：： AddRef** 和 **IUnknown：： Release** 来控制断点的生存期。 这些方法不会影响断点的生存期。 相反，在调用方法 [**了 removebreakpoint 时**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-removebreakpoint)后， **IDebugBreakpoint** 对象将被删除。

 

创建断点时，将为其提供唯一的 *断点 ID*。 此标识符将不会更改。 但是，断点删除后，其 ID 可用于另一个断点。 有关如何接收删除断点的通知的详细信息，请参阅 [监视事件](monitoring-events.md)。

创建断点时，它最初处于禁用状态;这意味着它不会导致目标停止执行。 可以通过使用方法 [**AddFlags**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugbreakpoint2-addflags) 添加启用了调试断点的标志来启用此断点 \_ \_ 。

第一次创建断点时，它具有与之关联的内存位置0x00000000。 可以通过使用 [**SetOffset**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugbreakpoint2-setoffset) 和地址来更改该位置，也可以通过将 [**SetOffsetExpression**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugbreakpoint2-setoffsetexpression) 与符号表达式结合使用来更改该位置。 断点的位置应在使用前更改为其初始值。

 

