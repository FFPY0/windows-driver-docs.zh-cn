---
title: SIO_ADDRESS_LIST_CHANGE
description: SIO_ADDRESS_LIST_CHANGE
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 SIO_ADDRESS_LIST_CHANGE 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 014fd5d79b60e4a024b87f69dea2a71708e8e430
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792621"
---
# <a name="sio_address_list_change"></a>SIO \_ 地址 \_ 列表 \_ 更改


\_ \_ \_ 当套接字地址族的本地传输地址列表发生变化时，SIO 地址列表更改套接字 i/o 控制操作会通知 WSK 应用程序。 此套接字 i/o 控制操作适用于所有套接字类型。

若要在已更改套接字地址系列的本地传输地址列表时收到通知，WSK 应用程序使用以下参数调用 [**WskControlSocket**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_control_socket) 函数。

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
<td><p>SIO_ADDRESS_LIST_CHANGE</p></td>
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

在调用 **WskControlSocket** 函数时，WSK 应用程序必须指定一个指向 IRP 的指针，以通知对套接字地址系列的本地传输地址列表的更改。 WSK 子系统将为 IRP 排队，并返回 "挂起" 状态 \_ 。 如果对套接字地址系列的本地传输地址列表进行了更改，则 WSK 子系统完成 IRP。 调用 IRP 的完成例程后，WSK 应用程序可以使用 [**SIO \_ 地址 \_ 列表 \_ 查询**](sio-address-list-query.md) 套接字 i/o 控制操作来查询套接字地址系列的新本地传输地址列表。

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

 

