---
title: OID_GEN_DIRECTED_FRAMES_XMIT
description: 作为查询，OID_GEN_DIRECTED_FRAMES_XMIT OID 指定传输的未出现错误的定向数据包的数量。
ms.date: 11/01/2019
keywords: -从 Windows Vista 开始 OID_GEN_DIRECTED_FRAMES_XMIT 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 9329b450ff0e648c223a1198b5136805d4280bb9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833333"
---
# <a name="oid_gen_directed_frames_xmit"></a>OID \_ 生成 \_ 定向 \_ 帧 \_ XMIT


作为查询，OID 生成 \_ \_ 定向 \_ 帧 \_ XMIT oid 指定传输的未出现错误的定向数据包的数量。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
已过时。

<a href="" id="ndis-6-0-and-later-drivers"></a>NDIS 6.0 和更高版本驱动程序  
未请求。 请改用 [OID 生成 \_ \_ 统计信息](oid-gen-statistics.md) 。

<a href="" id="ndis-5-1-drivers"></a>NDIS 5.1 驱动程序  
可选。

<a href="" id="windows-xp"></a>Windows XP  
支持。

<a href="" id="ndis-5-1-drivers"></a>NDIS 5.1 驱动程序  
可选。

<a name="remarks"></a>备注
-------

计数与 RFC 2863 中所述的 *ifOutUcastPkts* 计数器完全相同。

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

 

