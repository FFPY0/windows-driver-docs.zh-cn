---
title: WDI_TLV_P2P_SEND_ACTION_REQUEST_FRAME_PARAMETERS
description: WDI_TLV_P2P_SEND_ACTION_REQUEST_FRAME_PARAMETERS 是一种 TLV，其中包含用于用 OID_WDI_TASK_P2P_SEND_REQUEST_ACTION_FRAME 发送 Wi-Fi 直接操作请求帧的参数。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_SEND_ACTION_REQUEST_FRAME_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: f4bb08fff0365c6276c3fbd5aa481778e03a7e6b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818149"
---
# <a name="wdi_tlv_p2p_send_action_request_frame_parameters"></a>WDI \_ TLV \_ P2P \_ 发送 \_ 操作 \_ 请求 \_ 帧 \_ 参数


WDI \_ tlv \_ P2P \_ 发送 \_ 操作 \_ 请求 \_ 帧 \_ 参数是一个 TLV，其中包含用于通过 [OID \_ WDI \_ 任务 \_ P2P \_ 发送 \_ 请求 \_ 操作 \_ 帧](./oid-wdi-task-p2p-send-request-action-frame.md)发送 Wi-Fi 直接操作请求帧的参数。

## <a name="tlv-type"></a>TLV 类型


0x8B

## <a name="length"></a>长度


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型                                                                    | 描述                                                                                                                    |
|-------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------|
| [**WDI \_ P2P \_ 操作 \_ 帧 \_ 类型**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_p2p_action_frame_type) | 要发送的请求的类型。                                                                                                   |
| [**WDI \_ MAC \_ 地址**](/windows-hardware/drivers/ddi/dot11wdi/ns-dot11wdi-_wdi_mac_address)                       | 目标对等设备的 MAC 地址。                                                                                     |
| UINT8                                                                   | 事务的直接对话框标记。                                                                                   |
| UINT32                                                                  | 发送超时。 发送操作帧的最长时间（以毫秒为单位）。                                                 |
| UINT32                                                                  | 确认后停留时间。 确认传入数据包后在侦听通道上保留的时间（以毫秒为单位）。 |

 

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

 

