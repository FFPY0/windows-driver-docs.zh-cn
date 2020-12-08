---
title: SIO_WSK_SET_SENDTO_ADDRESS
description: SIO_WSK_SET_SENDTO_ADDRESS
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 SIO_WSK_SET_SENDTO_ADDRESS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 1ad1b901bb3a11b216020197ef30b5bb891a69c2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825019"
---
# <a name="sio_wsk_set_sendto_address"></a>SIO \_ WSK \_ 设置 \_ SENDTO \_ 地址


SIO \_ WSK \_ SET \_ SENDTO \_ ADDRESS socket I/O control 操作允许 WSK 应用程序为数据报套接字指定固定目标传输地址。 此套接字 i/o 控制操作仅适用于数据报套接字。

如果 WSK 应用程序为数据报套接字设置固定目标传输地址，则通过套接字发送的所有数据报都将发送到固定目标传输地址。 但是，将从任何传输地址接受套接字上收到的数据报。

WSK 应用程序可以在调用 [**WskSendTo**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_send_to)函数时，通过在 *RemoteAddress* 参数中指定备用远程传输地址来覆盖固定目标传输地址。 在这种情况下，将数据报发送到备用远程传输地址，而不是固定目标传输地址。

如果 WSK 应用程序使用此套接字 i/o 控制操作来指定固定目标传输地址，则必须在数据报套接字绑定到本地传输地址后执行此操作。

若要为数据报套接字设置固定目标传输地址，WSK 应用程序需要使用以下参数调用 [**WskControlSocket**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket) 函数。

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
<td><p><strong>WskIoctl</strong></p></td>
</tr>
<tr class="even">
<td><p><em>ControlCode</em></p></td>
<td><p>SIO_WSK_SET_SENDTO_ADDRESS</p></td>
</tr>
<tr class="odd">
<td><p><em>级别</em></p></td>
<td><p>0</p></td>
</tr>
<tr class="even">
<td><p><em>InputSize</em></p></td>
<td><p><em>InputBuffer</em>参数指向的 SOCKADDR 结构的大小。</p></td>
</tr>
<tr class="odd">
<td><p><em>InputBuffer</em></p></td>
<td><p>指向结构的指针，该结构指定数据报套接字的固定目标传输地址。 指针必须是指向特定 SOCKADDR 结构类型的指针，该类型对应于在创建数据报套接字时指定 WSK 应用程序的地址族。</p></td>
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


若要清除数据报套接字的固定目标传输地址，WSK 应用程序需要使用以下参数调用 **WskControlSocket** 函数。

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
<td><p><strong>WskIoctl</strong></p></td>
</tr>
<tr class="even">
<td><p><em>ControlCode</em></p></td>
<td><p>SIO_WSK_SET_SENDTO_ADDRESS</p></td>
</tr>
<tr class="odd">
<td><p><em>级别</em></p></td>
<td><p>0</p></td>
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



调用 **WskControlSocket** 函数为数据报套接字设置或清除固定目标传输地址时，WSK 应用程序必须指定一个指向 IRP 的指针。

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
<td>Wsk (包含 Wsk) </td>
</tr>
</tbody>
</table>

 

