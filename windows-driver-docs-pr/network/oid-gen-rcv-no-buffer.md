---
title: OID_GEN_RCV_NO_BUFFER
description: 作为查询，OID_GEN_RCV_NO_BUFFER OID 指定 NIC 由于缺少 NIC 接收缓冲区空间而无法接收的帧数。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_RCV_NO_BUFFER 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f3e5645f1d30631ec6753a33ac76f4f56f58a07e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836751"
---
# <a name="oid_gen_rcv_no_buffer"></a>OID \_ 生成 \_ RCV \_ 无 \_ 缓冲区


作为查询，OID \_ GEN \_ RCV \_ NO \_ buffer oid 指定 nic 由于缺少 nic 接收缓冲区空间而无法接收的帧数。 某些 Nic 未提供精确的丢失帧数;它们仅提供至少一个帧丢失的次数。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
已过时。

<a href="" id="ndis-6-0-and-later-drivers"></a>NDIS 6.0 和更高版本驱动程序  
未请求。 请改用 [OID 生成 \_ \_ 统计信息](oid-gen-statistics.md) 。

<a href="" id="ndis-5-1-drivers"></a>NDIS 5.1 驱动程序  
必需。

<a href="" id="windows-xp"></a>Windows XP  
支持。

<a href="" id="ndis-5-1-drivers"></a>NDIS 5.1 驱动程序  
必需。

<a name="remarks"></a>备注
-------

有关统计信息 Oid 的一般信息，请参阅 [常规统计](./ndis-general-statistics-oids.md)信息。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[OID \_ 生成 \_ 统计信息](oid-gen-statistics.md)

 

