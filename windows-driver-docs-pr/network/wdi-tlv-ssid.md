---
title: WDI_TLV_SSID
description: WDI_TLV_SSID 是包含 SSID 的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_SSID 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: be014d3cfd708d50aeed2e3d90953eec979b1884
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834159"
---
# <a name="wdi_tlv_ssid"></a>WDI \_ TLV \_ SSID


WDI \_ tlv \_ ssid 是包含 SSID 的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x3B

## <a name="length"></a>长度


UINT8 元素数组的大小 (以字节为单位) 。 允许数组长度为0。

## <a name="values"></a>值


| 类型      | 描述                                        |
|-----------|----------------------------------------------------|
| UINT8\[\] | 指定 SSID 的 UINT8 元素的数组。 |

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>最低受支持的客户端</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




