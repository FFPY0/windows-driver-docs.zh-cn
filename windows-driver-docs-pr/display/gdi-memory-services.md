---
title: GDI 内存服务
description: GDI 内存服务
keywords:
- GDI WDK Windows 2000 显示，内存服务
- 图形驱动程序 WDK Windows 2000 显示，内存服务
- 绘制 WDK GDI，内存服务
- 内存 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e08846ca0c7b77702b255db6ad181d7bf15a515e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819593"
---
# <a name="gdi-memory-services"></a>GDI 内存服务


## <span id="ddk_gdi_memory_services_gg"></span><span id="DDK_GDI_MEMORY_SERVICES_GG"></span>


GDI 为驱动程序编写器提供了多个与内存相关的服务，包括分配和释放系统内存、用户内存、专用用户内存和视频内存的功能，以及锁定和解锁内存范围的功能。 下表列出了 GDI 内存服务。

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
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engallocmem" data-raw-source="[&lt;strong&gt;EngAllocMem&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engallocmem)"><strong>EngAllocMem</strong></a></p></td>
<td align="left"><p>分配内存块，并在分配之前插入调用方提供的标记。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engallocprivateusermem" data-raw-source="[&lt;strong&gt;EngAllocPrivateUserMem&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engallocprivateusermem)"><strong>EngAllocPrivateUserMem</strong></a></p></td>
<td align="left"><p>从指定进程的地址空间分配一个专用用户内存块，并在分配之前插入一个调用方提供的标记。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engallocusermem" data-raw-source="[&lt;strong&gt;EngAllocUserMem&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engallocusermem)"><strong>EngAllocUserMem</strong></a></p></td>
<td align="left"><p>从当前进程的地址空间分配内存块，并在分配之前插入调用方提供的标记。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engfreemem" data-raw-source="[&lt;strong&gt;EngFreeMem&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engfreemem)"><strong>EngFreeMem</strong></a></p></td>
<td align="left"><p>释放由 <a href="/windows/win32/api/winddi/nf-winddi-engallocmem" data-raw-source="[&lt;strong&gt;EngAllocMem&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engallocmem)"><strong>EngAllocMem</strong></a>分配的系统内存块。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engfreeprivateusermem" data-raw-source="[&lt;strong&gt;EngFreePrivateUserMem&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engfreeprivateusermem)"><strong>EngFreePrivateUserMem</strong></a></p></td>
<td align="left"><p>释放由 <a href="/windows/win32/api/winddi/nf-winddi-engallocprivateusermem" data-raw-source="[&lt;strong&gt;EngAllocPrivateUserMem&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engallocprivateusermem)"><strong>EngAllocPrivateUserMem</strong></a>分配的专用用户内存块。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engfreeusermem" data-raw-source="[&lt;strong&gt;EngFreeUserMem&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engfreeusermem)"><strong>EngFreeUserMem</strong></a></p></td>
<td align="left"><p>释放由 <a href="/windows/win32/api/winddi/nf-winddi-engallocusermem" data-raw-source="[&lt;strong&gt;EngAllocUserMem&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engallocusermem)"><strong>EngAllocUserMem</strong></a>分配的用户内存块。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engsecuremem" data-raw-source="[&lt;strong&gt;EngSecureMem&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engsecuremem)"><strong>EngSecureMem</strong></a></p></td>
<td align="left"><p>锁定内存中指定的地址范围。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-engunsecuremem" data-raw-source="[&lt;strong&gt;EngUnsecureMem&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-engunsecuremem)"><strong>EngUnsecureMem</strong></a></p></td>
<td align="left"><p>解锁锁定的内存地址范围。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/dmemmgr/nf-dmemmgr-heapvidmemallocaligned" data-raw-source="[&lt;strong&gt;HeapVidMemAllocAligned&lt;/strong&gt;](/windows/win32/api/dmemmgr/nf-dmemmgr-heapvidmemallocaligned)"><strong>HeapVidMemAllocAligned</strong></a></p></td>
<td align="left"><p>使用 DirectDraw 视频内存堆管理器为显示驱动程序分配 <em>屏外内存</em> 。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/dmemmgr/nf-dmemmgr-vidmemfree" data-raw-source="[&lt;strong&gt;VidMemFree&lt;/strong&gt;](/windows/win32/api/dmemmgr/nf-dmemmgr-vidmemfree)"><strong>VidMemFree</strong></a></p></td>
<td align="left"><p>通过 <a href="/windows/win32/api/dmemmgr/nf-dmemmgr-heapvidmemallocaligned" data-raw-source="[&lt;strong&gt;HeapVidMemAllocAligned&lt;/strong&gt;](/windows/win32/api/dmemmgr/nf-dmemmgr-heapvidmemallocaligned)"><strong>HeapVidMemAllocAligned</strong></a>释放为显示驱动程序分配的屏幕内存。</p></td>
</tr>
</tbody>
</table>

 

