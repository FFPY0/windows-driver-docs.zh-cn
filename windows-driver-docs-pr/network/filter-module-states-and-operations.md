---
title: 筛选器模块状态和操作
description: 筛选器模块状态和操作
keywords:
- 筛选器驱动程序 WDK 网络，状态
- NDIS 筛选器驱动程序 WDK，状态
- 状态 WDK NDIS 筛选器
- 分离状态 WDK 网络
- 附加状态 WDK 网络
- 暂停状态 WDK 网络
- 正在重启状态 WDK 网络
- 运行状态 WDK ne
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eaa0bbcc3ed9abfd6ff3972dc8b2cf1f47f8e677
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840913"
---
# <a name="filter-module-states-and-operations"></a>筛选器模块状态和操作





筛选器驱动程序必须支持驱动程序所管理) 的筛选器驱动程序的每个筛选器模块 (实例的下列操作状态：

<a href="" id="detached"></a>已分离  
*分离* 状态是筛选器模块的初始状态。 当筛选器模块处于此状态时，NDIS 可以调用筛选器驱动程序的 [*FilterAttach*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach) 函数将筛选器模块附加到驱动程序堆栈。

<a href="" id="attaching"></a>附加  
在 *附加* 状态下，筛选器驱动程序准备将筛选器模块附加到驱动程序堆栈。

<a href="" id="paused"></a>悬停  
在 *暂停* 状态下，筛选器驱动程序不执行发送或接收操作。

<a href="" id="restarting"></a>重新  
在 *重新启动* 状态下，筛选器驱动程序完成为筛选器模块重新启动发送和接收操作所需的任何操作。

<a href="" id="running"></a>正在运行  
在 " *正在运行* " 状态下，筛选器驱动程序将执行筛选器模块的正常发送和接收处理。

<a href="" id="pausing"></a>暂停  
在 *暂停* 状态下，筛选器驱动程序完成为筛选器模块停止发送和接收操作所需的任何操作。

在下表中，标题是筛选器模块状态。 主要事件在第一列中列出。 表中的其余条目指定在某个状态下发生事件后筛选器模块进入的下一个状态。 空白条目表示无效的事件/状态组合。

<table style="width:100%;">
<colgroup>
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
<col width="14%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">事件/状态</th>
<th align="left">已分离</th>
<th align="left">附加</th>
<th align="left">已暂停</th>
<th align="left">重新启动</th>
<th align="left">正在运行</th>
<th align="left">正在暂停</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>筛选器附加</p></td>
<td align="left"><p>附加</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>附加完成</p></td>
<td align="left"></td>
<td align="left"><p>已暂停</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>筛选器分离</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>已分离</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>筛选器重新启动</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>重新启动</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>重新启动已完成</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>正在运行</p></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>筛选器暂停</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>正在暂停</p></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>暂停完成</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>已暂停</p></td>
</tr>
<tr class="even">
<td align="left"><p>附加失败</p></td>
<td align="left"></td>
<td align="left"><p>已分离</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="odd">
<td align="left"><p>重新启动失败</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>已暂停</p></td>
<td align="left"></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p>发送和接收</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>正在运行</p></td>
<td align="left"><p>正在暂停</p></td>
</tr>
<tr class="odd">
<td align="left"><p>OID 请求</p></td>
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>已暂停</p></td>
<td align="left"><p>重新启动</p></td>
<td align="left"><p>正在运行</p></td>
<td align="left"><p>正在暂停</p></td>
</tr>
</tbody>
</table>

 

主要筛选器驱动程序事件定义如下：

<a href="" id="--------filter-attach--------"></a> 筛选器附加   
NDIS 调用了驱动程序的 [*FilterAttach*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach) 函数，以将筛选器模块附加到驱动程序堆栈。 有关附加筛选器模块的详细信息，请参阅 [附加筛选器模块](attaching-a-filter-module.md)。

<a href="" id="attach-is-complete"></a>附加完成  
当筛选器模块处于 *附加* 状态并且筛选器驱动程序完成了筛选器模块所需的所有资源的初始化时，筛选器模块将进入 *暂停* 状态。

<a href="" id="--------filter-detach--------"></a> 筛选器分离   
NDIS 调用驱动程序的 [*FilterDetach*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_detach) 函数，以从驱动程序堆栈分离筛选器模块。 有关详细信息，请参阅 [分离筛选器模块](detaching-a-filter-module.md)。

<a href="" id="--------filter-restart--------"></a> 筛选器重新启动   
NDIS 调用驱动程序的 [*FilterRestart*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_restart) 函数来重新启动暂停的筛选器模块。 有关详细信息，请参阅 [启动筛选器模块](starting-a-filter-module.md)。

<a href="" id="restart-is-complete"></a>重新启动已完成  
当筛选器模块处于 *重新启动* 状态并且驱动程序已准备好执行发送和接收操作时，筛选器模块将进入 " *正在运行* " 状态。

<a href="" id="--------filter-pause--------"></a> 筛选器暂停   
NDIS 调用驱动程序的 [*FilterPause*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_pause) 函数来暂停筛选器模块。 有关详细信息，请参阅 [暂停筛选器模块](pausing-a-filter-module.md)。

<a href="" id="pause-is-complete"></a>暂停完成  
驱动程序完成停止发送和接收操作所需的所有操作后，暂停操作完成，筛选器模块处于 *暂停* 状态。

<a href="" id="attach-failed"></a>附加失败  
如果 NDIS 调用驱动程序的 [*FilterAttach*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_attach) 函数，并且附加操作失败 (例如，因为所需的资源) 不可用，则筛选器模块将返回到已 *分离* 状态。

<a href="" id="restart-failed"></a>重新启动失败  
如果 NDIS 调用驱动程序的 [*FilterRestart*](/windows-hardware/drivers/ddi/ndis/nc-ndis-filter_restart) 函数，并且重新启动尝试失败，则筛选器模块将返回到 "已 *暂停* " 状态。

<a href="" id="send-and-receive-operations"></a>发送和接收操作  
驱动程序可以在 *正在运行和正在**暂停* 的状态处理发送和接收操作。 有关发送和接收操作的详细信息，请参阅 [筛选模块发送和接收操作](filter-module-send-and-receive-operations.md)。

<a href="" id="oid-requests"></a>OID 请求  
驱动程序可以在 *正在运行、正在**重新启动*、已 *暂停* 和正在 *暂停* 的状态处理 OID 请求。 有关 OID 请求的详细信息，请参阅 [筛选器模块 OID 请求](filter-module-oid-requests.md)。

 

