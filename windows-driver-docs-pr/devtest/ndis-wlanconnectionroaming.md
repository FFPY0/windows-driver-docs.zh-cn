---
title: WlanConnectionRoaming 规则 (ndis)
description: WlanConnectionRoaming 规则验证微型端口驱动程序正确地遵循本机 802.11 无线 LAN (WLAN) 连接和漫游序列。
ms.assetid: 7DB1881B-4DD8-4E06-AAF2-C6EAD0EEC5FC
ms.date: 05/21/2018
keywords:
- WlanConnectionRoaming 规则 (ndis)
topic_type:
- apiref
api_name:
- WlanConnectionRoaming
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2fcf284c92c6f288d3118e341a6edc727f72bba5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522963"
---
# <a name="wlanconnectionroaming-rule-ndis"></a>WlanConnectionRoaming 规则 (ndis)


**WlanConnectionRoaming**规则验证微型端口驱动程序正确地遵循本机 802.11 无线 LAN (WLAN) 连接和漫游序列。

|              |      |
|--------------|------|
| 驱动程序模型 | NDIS |

|                                   |                                                                                                                                        |
|-----------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| 使用此规则发现的错误检查 | [**Bug 检查 0xC4:驱动程序\_VERIFIER\_已检测\_冲突**](https://msdn.microsoft.com/library/windows/hardware/ff560187) (0x00093005) |

<a name="how-to-test"></a>如何测试
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在运行时</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>运行<a href="https://msdn.microsoft.com/library/windows/hardware/ff545448" data-raw-source="[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)">Driver Verifier</a> ，然后选择<a href="https://msdn.microsoft.com/library/windows/hardware/hh454208" data-raw-source="[NDIS/WIFI verification](https://msdn.microsoft.com/library/windows/hardware/hh454208)">NDIS/WIFI 验证</a>选项。</p></td>
</tr>
</tbody>
</table>

 

<a name="applies-to"></a>适用于
----------

[**MiniportHaltEx**](https://msdn.microsoft.com/library/windows/hardware/ff559388)
[**NdisMIndicateStatusEx**](https://msdn.microsoft.com/library/windows/hardware/ff563600) See also
--------

[常规连接操作指南](https://msdn.microsoft.com/library/windows/hardware/ff552458)
[NDIS\_状态\_DOT11\_连接\_启动](https://msdn.microsoft.com/library/windows/hardware/ff567328)
[OID\_DOT11\_重置\_请求](https://msdn.microsoft.com/library/windows/hardware/ff569409)
[NDIS\_状态\_DOT11\_漫游\_开始](https://msdn.microsoft.com/library/windows/hardware/ff567360)
 

 




