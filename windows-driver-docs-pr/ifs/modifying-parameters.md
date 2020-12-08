---
title: 修改参数
description: 修改参数
keywords:
- 筛选器管理器 WDK 文件系统微筛选器，修改参数
- 交换缓冲 WDK 文件系统微筛选器
- 缓冲 WDK 文件系统微筛选器
- 内存描述符列出 WDK 文件系统微筛选器
- MDLs WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 19290ab63f4950feeb2933fdb96774e5f303939f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821457"
---
# <a name="modifying-parameters"></a>修改参数


微筛选器驱动程序可以修改与 i/o 操作相关联的某些参数，例如目标实例、目标文件对象和特定于操作的参数，包括 (MDL) 地址的缓冲区地址和内存描述符列表。 微筛选器驱动程序通常会在其 preoperation 回调中修改 i/o 请求的参数。 如果微筛选器驱动程序修改参数，则必须调用 [**FltSetCallbackDataDirty**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsetcallbackdatadirty) 来通知筛选器管理器参数已更改。 它还应记录从其 preoperation 回调传递的上下文中的更改，使其可用于其 postoperation 回调。

微筛选器驱动程序可在其 preoperation 回调中完成操作时更改操作的 i/o 状态，或在其 postoperation (回调中使操作失败，例如将状态 \_ 成功更改为错误状态) 。 在这种情况下，不需要调用 [**FltSetCallbackDataDirty**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsetcallbackdatadirty) 。

有关修改参数的详细信息，请参阅 [修改 I/o 操作的参数](modifying-the-parameters-for-an-i-o-operation.md)。

微筛选器驱动程序可以 "交换缓冲区"，只需将 i/o 请求的缓冲区字段替换为其自己的缓冲区。 此类微筛选器驱动程序负责保持 i/o 请求的 MDL 和缓冲字段同步。筛选器管理器 \_ \_ \_ \_ \_ 在 [**FLT \_ 回调 \_ 数据**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data) 结构中设置 FLTFL 回调数据系统缓冲区标志，以指示缓冲区是否为系统缓冲区; 如果是这样，则微筛选器驱动程序必须从非分页池分配替换缓冲区，并将 MDL 字段设置为 **NULL**。 否则，可以从分页或非分页池分配缓冲区，并且微筛选器驱动程序必须始终创建并设置 MDL。  (在执行快速 i/o 操作的情况下，可以从分页或非分页池分配新缓冲区，并且 MDL 应为 **NULL**。 ) 微筛选器驱动程序不能释放它所替换的缓冲区或 mdl，并且它不能释放已成功插入回回数据 (结构的 mdl，因为筛选器管理器将代表微身份筛选器驱动程序) 释放 mdl。 更改 MDL 或缓冲区后，微筛选器驱动程序必须调用 [**FltSetCallbackDataDirty**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsetcallbackdatadirty)。

微筛选器驱动程序必须为其交换缓冲区的任何操作注册 postoperation 回调。 在此回调例程中，微筛选器驱动程序必须释放它所分配的任何缓冲区。 筛选器管理器将释放 MDL，除非微筛选器驱动程序调用 [**FltRetainSwappedBufferMdlAddress**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltretainswappedbuffermdladdress);在这种情况下，微筛选器驱动程序负责释放 MDL。 微筛选器驱动程序可以调用 [**FltGetSwappedBufferMdlAddress**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetswappedbuffermdladdress) 来获取 preoperation 回调中的缓冲区集的 MDL。

如果微筛选器驱动程序在其交换缓冲区的操作过程中被卸载，则无法 "排出" 该操作;相反，操作将被取消，筛选器管理器将等待操作完成，然后再卸载微筛选器驱动程序。

有关交换缓冲区的微筛选器驱动程序的示例，请参阅 SwapBuffers 示例。

### <a name="span-idfilter_manager_routines_for_modifying_parametersspanspan-idfilter_manager_routines_for_modifying_parametersspanspan-idfilter_manager_routines_for_modifying_parametersspanfilter-manager-routines-for-modifying-parameters"></a><span id="Filter_Manager_Routines_for_Modifying_Parameters"></span><span id="filter_manager_routines_for_modifying_parameters"></span><span id="FILTER_MANAGER_ROUTINES_FOR_MODIFYING_PARAMETERS"></span>用于修改参数的筛选器管理器例程

筛选器管理器提供以下支持例程，用于在 preoperation 和 postoperation 回调例程中修改 i/o 操作参数：

[**FltClearCallbackDataDirty**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltclearcallbackdatadirty)

[**FltIsCallbackDataDirty**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltiscallbackdatadirty)

[**FltSetCallbackDataDirty**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsetcallbackdatadirty)

以下例程为交换缓冲区提供支持：

[**FltGetSwappedBufferMdlAddress**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltgetswappedbuffermdladdress)

[**FltRetainSwappedBufferMdlAddress**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltretainswappedbuffermdladdress)

 

