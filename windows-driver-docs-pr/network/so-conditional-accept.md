---
title: SO_CONDITIONAL_ACCEPT
description: SO_CONDITIONAL_ACCEPT
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 SO_CONDITIONAL_ACCEPT 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: fb0842bce7b3a5b23f82079b5621cf90336e0600
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825009"
---
# <a name="so_conditional_accept"></a>SO \_ 条件 \_ 接受


" \_ 条件 \_ 接受套接字" 选项的状态确定是否在侦听套接字上启用条件接受模式。 此套接字选项仅适用于侦听套接字。

如果 WSK 应用程序设置此套接字选项，则必须在侦听套接字绑定到本地传输地址之前执行此操作。

若要设置此套接字选项的状态，WSK 应用程序需要使用以下参数调用 [**WskControlSocket**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket) 函数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>参数</th>
<th>“值”</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>RequestType</em></p></td>
<td><p><strong>WskSetOption</strong></p></td>
</tr>
<tr class="even">
<td><p><em>ControlCode</em></p></td>
<td><p>SO_CONDITIONAL_ACCEPT</p></td>
</tr>
<tr class="odd">
<td><p><em>级别</em></p></td>
<td><p>SOL_SOCKET</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>sizeof (ULONG) </p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>指向 ULONG 类型的变量的指针，该变量包含套接字选项的新状态值：</p>
<p>0：禁用条件接受模式</p>
<p>1：启用条件接受模式</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSize</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>Null</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>Null</p></td>
</tr>
</tbody>
</table>


若要检索此 socket 选项的状态，WSK 应用程序需要使用以下参数调用 **WskControlSocket** 函数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>参数</th>
<th>“值”</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>RequestType</em></p></td>
<td><p><strong>WskGetOption</strong></p></td>
</tr>
<tr class="even">
<td><p><em>ControlCode</em></p></td>
<td><p>SO_CONDITIONAL_ACCEPT</p></td>
</tr>
<tr class="odd">
<td><p><em>级别</em></p></td>
<td><p>SOL_SOCKET</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>Null</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSize</em></p></td>
<td><p>sizeof (ULONG) </p></td>
</tr>
<tr class="odd">
<td><p><em>OutputBuffer</em></p></td>
<td><p>指向 ULONG 类型的变量的指针，该变量接收 socket 选项的状态值：</p>
<p>0：已禁用条件接受模式</p>
<p>1：条件接受模式已启用</p></td>
</tr>
<tr class="even">
<td><p><em>OutputSizeReturned</em></p></td>
<td><p>Null</p></td>
</tr>
</tbody>
</table>



调用 **WskControlSocket** 函数时，WSK 应用程序必须指定一个指向 IRP 的指针，以便设置或检索 SO \_ 条件 \_ 接受套接字选项的状态。

此套接字选项的默认状态是禁用条件接受模式。

某些传输协议可能不支持侦听套接字上的条件接受模式。

有关有条件地接受传入连接的详细信息，请参阅 [侦听和接受传入连接](./listening-for-and-accepting-incoming-connections.md)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>在 Windows Vista 和更高版本的 Windows 操作系统中可用。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ws2def (包含 Wsk) </td>
</tr>
</tbody>
</table>

 

