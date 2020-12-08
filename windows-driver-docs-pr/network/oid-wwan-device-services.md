---
title: OID_WWAN_DEVICE_SERVICES
description: OID_WWAN_DEVICE_SERVICES 返回微型端口驱动程序所支持的设备服务的列表。NDIS_WWAN_DEVICE_SERVICES 结构，它指示受支持的设备服务 Guid。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_DEVICE_SERVICES 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 1513fee7ecd422e3c6fb5904c23b5c1b7e0449d3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823837"
---
# <a name="oid_wwan_device_services"></a>OID \_ WWAN \_ 设备 \_ 服务


OID \_ WWAN \_ 设备 \_ 服务返回微型端口驱动程序所支持的设备服务的列表。

微型端口驱动程序必须异步处理查询请求，最初 \_ 返回 \_ \_ 原始请求所需的 ndis 状态指示，稍后发送 ndis \_ 状态 \_ WWAN \_ 设备 \_ 服务状态通知，其中包含表示支持的设备服务 guid 的 [**ndis \_ WWAN \_ 设备 \_**](/windows-hardware/drivers/ddi/_netvista/) 服务结构。

不支持设置请求。

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
<td><p>版本：在 windows 8 及更高版本的 Windows 中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

 

