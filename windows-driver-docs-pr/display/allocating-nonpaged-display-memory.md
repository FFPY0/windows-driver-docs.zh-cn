---
title: 分配非分页显示内存
description: 分配非分页显示内存
keywords:
- 非分页显示内存 WDK DirectX 9。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1eaccf54dad9552687e86850dc8dcdeabf73bb5a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810517"
---
# <a name="allocating-nonpaged-display-memory"></a>分配非分页显示内存


## <span id="ddk_allocating_nonpaged_display_memory_gg"></span><span id="DDK_ALLOCATING_NONPAGED_DISPLAY_MEMORY_GG"></span>


**本主题仅适用于 Microsoft Windows XP 和更高版本。**

DirectX 9.0 版本显示驱动程序可以调用 [**EngAllocMem**](/windows/win32/api/winddi/nf-winddi-engallocmem) 图形设备接口 (GDI) 函数，不仅可以从系统的分页池分配内存，还可以从非分页池分配内存。 若要分配非分页内存，驱动程序必须 \_ \_ 在 **EngAllocMem** 调用的 *Flags* 参数中指定 FL 非分页内存标志。 如果未指定此标志，则将从系统的分页池分配内存。

Windows 2000 及更早版本仅允许从系统的分页池进行分配。

尽管 WindowsXP 和更高版本中提供了此功能，但在 Windows XP 和 Windows XP Service Pack 1 (SP1) Ddk 中没有记录此功能。

 

