---
title: GDI 信号灯服务
description: GDI 信号灯服务
keywords:
- GDI WDK Windows 2000 显示，信号服务
- 图形驱动程序 WDK Windows 2000 显示，信号服务
- 绘制 WDK GDI，信号服务
- 信号灯
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7980c1df55bbed947c116bba26b1b935ee1c6ae2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793953"
---
# <a name="gdi-semaphore-services"></a>GDI 信号灯服务


## <span id="ddk_gdi_semaphore_services_gg"></span><span id="DDK_GDI_SEMAPHORE_SERVICES_GG"></span>


GDI 提供与信号和安全信号量相关的服务选择。 驱动程序可以使用这些服务来创建或删除信号量，以及获取或释放信号量。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">函数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engacquiresemaphore" data-raw-source="[&lt;strong&gt;EngAcquireSemaphore&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engacquiresemaphore)"><strong>EngAcquireSemaphore</strong></a></p></td>
<td align="left"><p>获取与信号量关联的资源，以供调用线程独占访问。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engcreatesemaphore" data-raw-source="[&lt;strong&gt;EngCreateSemaphore&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engcreatesemaphore)"><strong>EngCreateSemaphore</strong></a></p></td>
<td align="left"><p>创建信号灯对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engdeletesafesemaphore" data-raw-source="[&lt;strong&gt;EngDeleteSafeSemaphore&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engdeletesafesemaphore)"><strong>EngDeleteSafeSemaphore</strong></a></p></td>
<td align="left"><p>删除对指定安全信号量的引用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engdeletesemaphore" data-raw-source="[&lt;strong&gt;EngDeleteSemaphore&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engdeletesemaphore)"><strong>EngDeleteSemaphore</strong></a></p></td>
<td align="left"><p>从系统资源列表中删除信号灯对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-enginitializesafesemaphore" data-raw-source="[&lt;strong&gt;EngInitializeSafeSemaphore&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-enginitializesafesemaphore)"><strong>EngInitializeSafeSemaphore</strong></a></p></td>
<td align="left"><p>初始化指定的安全信号量。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engissemaphoreowned" data-raw-source="[&lt;strong&gt;EngIsSemaphoreOwned&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engissemaphoreowned)"><strong>EngIsSemaphoreOwned</strong></a></p></td>
<td align="left"><p>确定任何线程是否持有指定的信号量。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engissemaphoreownedbycurrentthread" data-raw-source="[&lt;strong&gt;EngIsSemaphoreOwnedByCurrentThread&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engissemaphoreownedbycurrentthread)"><strong>EngIsSemaphoreOwnedByCurrentThread</strong></a></p></td>
<td align="left"><p>确定当前正在执行的线程是否持有指定的信号量。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engreleasesemaphore" data-raw-source="[&lt;strong&gt;EngReleaseSemaphore&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engreleasesemaphore)"><strong>EngReleaseSemaphore</strong></a></p></td>
<td align="left"><p>释放指定的信号量。</p></td>
</tr>
</tbody>
</table>

 

