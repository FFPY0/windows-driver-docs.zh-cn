---
title: WDI_TLV_P2P_ACTION_FRAME_RESPONSE_PARAMETERS
description: WDI_TLV_P2P_ACTION_FRAME_RESPONSE_PARAMETERS 是包含 Wi-Fi 直接操作帧响应参数的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_ACTION_FRAME_RESPONSE_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 7761f48aeca67bcc7da729f617094c9ddb61d144
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787153"
---
# <a name="wdi_tlv_p2p_action_frame_response_parameters"></a>WDI \_ TLV \_ P2P \_ 操作 \_ 帧 \_ 响应 \_ 参数


WDI \_ tlv \_ P2P \_ 操作 \_ 帧 \_ 响应 \_ 参数是一个 Tlv，其中包含 Wi-Fi 直接操作帧响应参数。

## <a name="tlv-type"></a>TLV 类型


0xAD

## <a name="length"></a>长度


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型                                                                    | 描述                                                                                                                          |
|-------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------|
| [**WDI \_ P2P \_ 操作 \_ 帧 \_ 类型**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_p2p_action_frame_type) | 要发送的响应帧的类型。                                                                                               |
| [**WDI \_ MAC \_ 地址**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)                       | 目标对等方 Wi-Fi Direct 设备的设备地址。                                                                           |
| UINT8                                                                   | 此事务的 Wi-Fi 直接对话框标记。                                                                                  |
| UINT32                                                                  | 发送超时。 指定发送此操作帧的最长时间（以毫秒为单位）。                                            |
| UINT32                                                                  | 确认后停留时间。 指定在确认传入数据包后，在侦听通道上保留的时间（以毫秒为单位）。 |

 

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

 

