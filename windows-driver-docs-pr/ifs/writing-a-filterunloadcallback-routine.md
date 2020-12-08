---
title: 编写 FilterUnloadCallback 例程
description: 编写 FilterUnloadCallback 例程
keywords:
- FilterUnloadCallback
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2cb24d86e97221754371d0c179d94cd67ccae7c0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785219"
---
# <a name="writing-a-filterunloadcallback-routine"></a>编写 FilterUnloadCallback 例程


## <span id="ddk_writing_a_filterunloadcallback_routine_if"></span><span id="DDK_WRITING_A_FILTERUNLOADCALLBACK_ROUTINE_IF"></span>


*FilterUnloadCallback* 例程定义如下：

```cpp
typedef NTSTATUS
(*PFLT_FILTER_UNLOAD_CALLBACK) (
    FLT_FILTER_UNLOAD_FLAGS Flags
    );
```

*FilterUnloadCallback* 例程有一个输入参数 *标志*，该参数可以为 **NULL** ，也可以是 FLTFL \_ 筛选器 \_ \_ 必需卸载。 筛选器管理器将此参数设置为 FLTFL \_ filter \_ \_ 必需的 unload，以指示卸载操作是必需的。 有关此参数的详细信息，请参阅 [**PFLT \_ 筛选器 \_ 卸载 \_ 回调**](/windows-hardware/drivers/ddi/fltkernel/nc-fltkernel-pflt_filter_unload_callback)。

微筛选器驱动程序的 *FilterUnloadCallback* 例程必须执行以下步骤：

-   关闭任何打开的内核模式通信服务器端口句柄。

-   调用 [**FltUnregisterFilter**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltunregisterfilter) 以注销微筛选器驱动程序。

-   执行任何所需的全局清除。

-   返回相应的 NTSTATUS 值。

本节包括：

[关闭通信服务器端口](closing-the-communication-server-port.md)

[正在注销微筛选器](unregistering-the-minifilter.md)

[执行全局清除](performing-global-cleanup.md)

[从 FilterUnloadCallback 例程返回状态](returning-status-from-a-filterunloadcallback-routine.md)

 

