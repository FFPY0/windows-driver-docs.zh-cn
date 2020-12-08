---
title: WDI_TLV_P2P_GO_NEGOTIATION_RESPONSE_PARAMETERS
description: WDI_TLV_P2P_GO_NEGOTIATION_RESPONSE_PARAMETERS 是包含传入的中转协商响应参数的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_GO_NEGOTIATION_RESPONSE_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: fdcd991f95503f0cf62501bc39ffff12bf3d12c8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819979"
---
# <a name="wdi_tlv_p2p_go_negotiation_response_parameters"></a>WDI \_ TLV \_ P2P \_ 中转 \_ 协商 \_ 响应 \_ 参数


WDI \_ tlv \_ P2P \_ 中转 \_ 协商 \_ 响应 \_ 参数是包含传入的中转协商响应参数的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x71

## <a name="length"></a>长度


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型                                              | 描述                                                                                                                                                                     |
|---------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT8                                             | 指定由 Wi-Fi Direct 规范定义的 Wi-Fi 直接状态代码。                                                                                           |
| UINT8                                             | 指定本地 Wi-Fi 直接执行意向。 这是一个介于0到15之间的值。                                                                                                   |
| UINT8                                             | 指定中转意向的 "断字符" 字段。                                                                                                                               |
| UINT16                                            | 指定中转配置超时值（以毫秒为单位）。                                                                                                                         |
| UINT16                                            | 指定客户端配置超时值（以毫秒为单位）。                                                                                                                     |
| [**WDI \_ MAC \_ 地址**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address) | 预期接口地址。 指定用于未来 Wi-Fi 直接连接的本地 MAC 地址。                                                                                 |
| UINT8                                             | 指定 Wi-Fi 的直接分组功能位掩码。 位掩码与 Wi-Fi P2P 技术规范的表13组功能位图定义中定义的位掩码匹配。 |
| UINT8                                             | 指定操作系统在上述组功能位图中设置的位。                                                                                            |

 

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

 

