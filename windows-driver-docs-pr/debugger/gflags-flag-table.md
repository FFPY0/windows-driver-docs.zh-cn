---
title: GFlags 标志表
description: GFlags 标志表
keywords:
- GFlags，标志表
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67f03b91fef1c53353e77dec2d163bef09417f47
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834731"
---
# <a name="gflags-flag-table"></a>GFlags 标志表


## <span id="ddk_gflags_flag_table_dtools"></span><span id="DDK_GFLAGS_FLAG_TABLE_DTOOLS"></span>


下表列出了 GFlags 更改的标志、每个标志的十六进制值和缩写，以及目标 (R 用于注册表，K 用于内核，I 表示标志有效的图像文件) 。

有关每个标志的详细说明，请参阅 [全局标志引用](global-flag-reference.md)。

有关使用 GFlags 的信息，请参阅 [GFlags 概述](gflags-overview.md) 和 [GFlags 详细信息](gflags-details.md)。

**重要提示**   池标记在 Windows Server 2003 和更高版本的 Windows 中被永久启用。 在这些系统中，"**全局标志**" 对话框中的 "**启用池标记**" 复选框将灰显，启用或禁用池标记的命令将失败。

 

**注意**  提供每个标志的符号名称只是为了参考。 由于符号名称发生更改，因此它们不是全局标志的可靠标识符。

 

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">描述</th>
<th align="left">符号名称</th>
<th align="left">十六进制值</th>
<th align="left">缩写</th>
<th align="left">目标</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="buffer-dbgprint-output.md" data-raw-source="[Buffer DbgPrint Output](buffer-dbgprint-output.md)">缓冲区 DbgPrint 输出</a></p></td>
<td align="left"><p>FLG_DISABLE_DBGPRINT</p></td>
<td align="left"><p>0x08000000</p></td>
<td align="left"><p>ddp</p></td>
<td align="left"><p>R，K</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="create-kernel-mode-stack-trace-database.md" data-raw-source="[Create kernel mode stack trace database](create-kernel-mode-stack-trace-database.md)">创建内核模式堆栈跟踪数据库</a></p></td>
<td align="left"><p>FLG_KERNEL_STACK_TRACE_DB</p></td>
<td align="left"><p>0x2000</p></td>
<td align="left"><p>kst</p></td>
<td align="left"><p>R</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="create-user-mode-stack-trace-database.md" data-raw-source="[Create user mode stack trace database](create-user-mode-stack-trace-database.md)">创建用户模式堆栈跟踪数据库</a></p></td>
<td align="left"><p>FLG_USER_STACK_TRACE_DB</p></td>
<td align="left"><p>0x1000</p></td>
<td align="left"><p>ust</p></td>
<td align="left"><p>R，K，I</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="debug-initial-command.md" data-raw-source="[Debug initial command](debug-initial-command.md)">调试初始命令</a></p></td>
<td align="left"><p>FLG_DEBUG_INITIAL_COMMAND</p></td>
<td align="left"><p>0x04</p></td>
<td align="left"><p>.dic</p></td>
<td align="left"><p>R</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="debug-winlogon.md" data-raw-source="[Debug WinLogon](debug-winlogon.md)">调试 WinLogon</a></p></td>
<td align="left"><p>FLG_DEBUG_INITIAL_COMMAND_EX</p></td>
<td align="left"><p>0x04000000</p></td>
<td align="left"><p>dwl</p></td>
<td align="left"><p>R</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="disable-heap-coalesce-on-free.md" data-raw-source="[Disable heap coalesce on free](disable-heap-coalesce-on-free.md)">释放时禁用堆合并</a></p></td>
<td align="left"><p>FLG_HEAP_DISABLE_COALESCING</p></td>
<td align="left"><p>0x00200000</p></td>
<td align="left"><p>dhc</p></td>
<td align="left"><p>R，K，I</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="disable-paging-of-kernel-stacks.md" data-raw-source="[Disable paging of kernel stacks](disable-paging-of-kernel-stacks.md)">禁用内核堆栈分页</a></p></td>
<td align="left"><p>FLG_DISABLE_PAGE_KERNEL_STACKS</p></td>
<td align="left"><p>0x080000</p></td>
<td align="left"><p>dps</p></td>
<td align="left"><p>R</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="disable-protected-dll-verification.md" data-raw-source="[Disable protected DLL verification](disable-protected-dll-verification.md)">禁用受保护的 DLL 验证</a></p></td>
<td align="left"><p>FLG_DISABLE_PROTDLLS</p></td>
<td align="left"><p>0x80000000</p></td>
<td align="left"><p>dpd</p></td>
<td align="left"><p>R，K，I</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="disable-stack-extension.md" data-raw-source="[Disable stack extension](disable-stack-extension.md)">禁用堆栈扩展</a></p></td>
<td align="left"><p>FLG_DISABLE_STACK_EXTENSION</p></td>
<td align="left"><p>0x010000</p></td>
<td align="left"><p>dse</p></td>
<td align="left"><p>I</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="early-critical-section-event-creation.md" data-raw-source="[Early critical section event creation](early-critical-section-event-creation.md)">提前创建关键节事件</a></p></td>
<td align="left"><p>FLG_CRITSEC_EVENT_CREATION</p></td>
<td align="left"><p>0x10000000</p></td>
<td align="left"><p>cse</p></td>
<td align="left"><p>R，K，I</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="enable-application-verifier.md" data-raw-source="[Enable application verifier](enable-application-verifier.md)">启用应用程序验证工具</a></p></td>
<td align="left"><p>FLG_APPLICATION_VERIFIER</p></td>
<td align="left"><p>0x0100</p></td>
<td align="left"><p>vrf</p></td>
<td align="left"><p>R，K，I</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="enable-bad-handles-detection.md" data-raw-source="[Enable bad handles detection](enable-bad-handles-detection.md)">启用错误句柄检测</a></p></td>
<td align="left"><p>FLG_ENABLE_HANDLE_EXCEPTIONS</p></td>
<td align="left"><p>0x40000000</p></td>
<td align="left"><p>bhd</p></td>
<td align="left"><p>R，K</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="enable-close-exception.md" data-raw-source="[Enable close exception](enable-close-exception.md)">启用关闭异常</a></p></td>
<td align="left"><p>FLG_ENABLE_CLOSE_EXCEPTIONS</p></td>
<td align="left"><p>0x400000</p></td>
<td align="left"><p>ece</p></td>
<td align="left"><p>R，K</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="enable-debugging-of-win32-subsystem.md" data-raw-source="[Enable debugging of Win32 subsystem](enable-debugging-of-win32-subsystem.md)">启用 Win32 子系统调试</a></p></td>
<td align="left"><p>FLG_ENABLE_CSRDEBUG</p></td>
<td align="left"><p>0x020000</p></td>
<td align="left"><p>d32</p></td>
<td align="left"><p>R</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="enable-exception-logging.md" data-raw-source="[Enable exception logging](enable-exception-logging.md)">启用异常日志记录</a></p></td>
<td align="left"><p>FLG_ENABLE_EXCEPTION_LOGGING</p></td>
<td align="left"><p>0x800000</p></td>
<td align="left"><p>eel</p></td>
<td align="left"><p>R，K</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="enable-heap-free-checking.md" data-raw-source="[Enable heap free checking](enable-heap-free-checking.md)">启用堆释放检查</a></p></td>
<td align="left"><p>FLG_HEAP_ENABLE_FREE_CHECK</p></td>
<td align="left"><p>0x20</p></td>
<td align="left"><p>hfc</p></td>
<td align="left"><p>R，K，I</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="enable-heap-parameter-checking.md" data-raw-source="[Enable heap parameter checking](enable-heap-parameter-checking.md)">启用堆参数检查</a></p></td>
<td align="left"><p>FLG_HEAP_VALIDATE_PARAMETERS</p></td>
<td align="left"><p>0x40</p></td>
<td align="left"><p>hpc</p></td>
<td align="left"><p>R，K，I</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="enable-heap-tagging.md" data-raw-source="[Enable heap tagging](enable-heap-tagging.md)">启用堆标记</a></p></td>
<td align="left"><p>FLG_HEAP_ENABLE_TAGGING</p></td>
<td align="left"><p>0x0800</p></td>
<td align="left"><p>htg</p></td>
<td align="left"><p>R，K，I</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="enable-heap-tagging-by-dll.md" data-raw-source="[Enable heap tagging by DLL](enable-heap-tagging-by-dll.md)">启用按 DLL 的堆标记</a></p></td>
<td align="left"><p>FLG_HEAP_ENABLE_TAG_BY_DLL</p></td>
<td align="left"><p>0x8000</p></td>
<td align="left"><p>htd</p></td>
<td align="left"><p>R，K，I</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="enable-heap-tail-checking.md" data-raw-source="[Enable heap tail checking](enable-heap-tail-checking.md)">启用堆尾部检查</a></p></td>
<td align="left"><p>FLG_HEAP_ENABLE_TAIL_CHECK</p></td>
<td align="left"><p>0x10</p></td>
<td align="left"><p>htc</p></td>
<td align="left"><p>R，K，I</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="enable-heap-validation-on-call.md" data-raw-source="[Enable heap validation on call](enable-heap-validation-on-call.md)">启用调用时进行堆验证</a></p></td>
<td align="left"><p>FLG_HEAP_VALIDATE_ALL</p></td>
<td align="left"><p>0x80</p></td>
<td align="left"><p>hvc</p></td>
<td align="left"><p>R，K，I</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="enable-loading-of-kernel-debugger-symbols.md" data-raw-source="[Enable loading of kernel debugger symbols](enable-loading-of-kernel-debugger-symbols.md)">启用内核调试程序符号加载</a></p></td>
<td align="left"><p>FLG_ENABLE_KDEBUG_SYMBOL_LOAD</p></td>
<td align="left"><p>0x040000</p></td>
<td align="left"><p>ksl</p></td>
<td align="left"><p>R，K</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="enable-object-handle-type-tagging.md" data-raw-source="[Enable object handle type tagging](enable-object-handle-type-tagging.md)">启用对象句柄类型标记</a></p></td>
<td align="left"><p>FLG_ENABLE_HANDLE_TYPE_TAGGING</p></td>
<td align="left"><p>0x01000000</p></td>
<td align="left"><p>eot</p></td>
<td align="left"><p>R，K</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="enable-page-heap.md" data-raw-source="[Enable page heap](enable-page-heap.md)">启用页堆</a></p></td>
<td align="left"><p>FLG_HEAP_PAGE_ALLOCS</p></td>
<td align="left"><p>0x02000000</p></td>
<td align="left"><p>hpa</p></td>
<td align="left"><p>R，K，I</p></td>
</tr>
<tr class="odd">
<td align="left"><p></p>仅 (Windows 2000 和 Windows XP
<a href="enable-pool-tagging.md" data-raw-source="[Enable pool tagging](enable-pool-tagging.md)">启用池标记</a>) </td>
<td align="left"><p>FLG_POOL_ENABLE_TAGGING</p></td>
<td align="left"><p>0x0400</p></td>
<td align="left"><p>ptg</p></td>
<td align="left"><p>R</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="enable-system-critical-breaks.md" data-raw-source="[Enable system critical breaks](enable-system-critical-breaks.md)">启用系统关键突破</a></p></td>
<td align="left"><p>FLG_ENABLE_SYSTEM_CRIT_BREAKS</p></td>
<td align="left"><p>0x100000</p></td>
<td align="left"><p>scb</p></td>
<td align="left"><p>R，K，I</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="load-image-using-large-pages-if-possible.md" data-raw-source="[Load image using large pages if possible](load-image-using-large-pages-if-possible.md)">在可能的情况下大型页加载映像</a></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>lpg</p></td>
<td align="left"><p>I</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="maintain-a-list-of-objects-for-each-type.md" data-raw-source="[Maintain a list of objects for each type](maintain-a-list-of-objects-for-each-type.md)">维护每个类型的对象列表</a></p></td>
<td align="left"><p>FLG_MAINTAIN_OBJECT_TYPELIST</p></td>
<td align="left"><p>0x4000</p></td>
<td align="left"><p>otl</p></td>
<td align="left"><p>R</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="enable-silent-process-exit-monitoring.md" data-raw-source="[Enable silent process exit monitoring](enable-silent-process-exit-monitoring.md)">启用静默进程退出监视</a></p></td>
<td align="left"><p>FLG_MONITOR_SILENT_PROCESS_EXIT</p></td>
<td align="left"><p>0x200</p></td>
<td align="left"></td>
<td align="left"><p>R</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="object-reference-tracing.md" data-raw-source="[Object Reference Tracing](object-reference-tracing.md)">对象引用跟踪</a></p>
<p> (Windows Vista 及更高版本) </p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>R，K</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="show-loader-snaps.md" data-raw-source="[Show loader snaps](show-loader-snaps.md)">显示加载器快照</a></p></td>
<td align="left"><p>FLG_SHOW_LDR_SNAPS</p></td>
<td align="left"><p>0x02</p></td>
<td align="left"><p>购买</p></td>
<td align="left"><p>R，K，I</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="special-pool.md" data-raw-source="[Special Pool](special-pool.md)">特殊池</a></p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>spp</p></td>
<td align="left"><p>R</p>
<p>R，K (Windows Vista 及更高版本) </p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="stop-on-exception.md" data-raw-source="[Stop on exception](stop-on-exception.md)">异常时停止</a></p></td>
<td align="left"><p>FLG_STOP_ON_EXCEPTION</p></td>
<td align="left"><p>0x01</p></td>
<td align="left"><p>soe</p></td>
<td align="left"><p>R，K，I</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="stop-on-hung-gui.md" data-raw-source="[Stop on hung GUI](stop-on-hung-gui.md)">GUI 挂起时停止</a></p></td>
<td align="left"><p>FLG_STOP_ON_HUNG_GUI</p></td>
<td align="left"><p>0x08</p></td>
<td align="left"><p>shg</p></td>
<td align="left"><p>K</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="stop-on-unhandled-user-mode-exception.md" data-raw-source="[Stop on unhandled user-mode exception](stop-on-unhandled-user-mode-exception.md)">出现未经处理的用户模式异常时停止</a></p></td>
<td align="left"><p>FLG_STOP_ON_UNHANDLED_EXCEPTION</p></td>
<td align="left"><p>0x20000000</p></td>
<td align="left"><p>sue</p></td>
<td align="left"><p>R，K，I</p></td>
</tr>
</tbody>
</table>

 

 

 





