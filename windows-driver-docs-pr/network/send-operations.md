---
title: 发送操作
description: 发送操作
keywords:
- 发送操作 WDK Native 802.11 IHV 扩展 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ddae4864a761a3abfd7ca015d84e9fa5cf1ee06e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840279"
---
# <a name="send-operations"></a>发送操作




 

当执行后连接操作时，通过调用 [*Dot11ExtIhvPerformPostAssociate*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate)启动，IHV 扩展 DLL 可以通过无线 LAN (WLAN) 适配器发送数据包。 有关后处理后操作的详细信息，请参阅 [之后的关联操作](post-association-operations.md)。

通常，DLL 使用通过 [**Dot11ExtSetAuthAlgorithm**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_auth_algorithm)启用的算法将安全数据包发送到访问点 (AP) 用于数据端口身份验证。 IHV 扩展 DLL 在预关联操作过程中调用 **Dot11ExtSetAuthAlgorithm** 。 有关此操作的详细信息，请参阅 [预关联操作](pre-association-operations.md)。

**注意**  对于 Windows Vista，IHV 扩展 DLL 仅支持基础结构基本服务集 (BSS) 网络。

 

发送数据包时，IHV 扩展 DLL 必须遵循这些准则。

-   IHV 扩展 DLL 必须为完整的802.11 数据包分配内存，包括 802.11 (MAC) 标头、LLC 封装 (如有必要) 和负载数据。

    下表描述了 802.11 MAC 标头中的哪些字段和子字段由 IHV 扩展 DLL 或 WLAN 适配器设置。

    <table>
    <colgroup>
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    <col width="25%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th align="left">字段名称</th>
    <th align="left">子字段名称</th>
    <th align="left">由 IHV 扩展 DLL 设置</th>
    <th align="left">由 WLAN 适配器设置</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td align="left"><p>框架控件</p></td>
    <td align="left"><p>协议版本</p></td>
    <td align="left"><p>X</p></td>
    <td align="left"></td>
    </tr>
    <tr class="even">
    <td align="left"><p>框架控件</p></td>
    <td align="left"><p>类型</p></td>
    <td align="left"><p>X</p></td>
    <td align="left"></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>框架控件</p></td>
    <td align="left"><p>子类型</p></td>
    <td align="left"><p>X</p></td>
    <td align="left"></td>
    </tr>
    <tr class="even">
    <td align="left"><p>框架控件</p></td>
    <td align="left"><p>到 DS</p></td>
    <td align="left"><p>X</p></td>
    <td align="left"></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>框架控件</p></td>
    <td align="left"><p>从 DS</p></td>
    <td align="left"><p>X</p></td>
    <td align="left"></td>
    </tr>
    <tr class="even">
    <td align="left"><p>框架控件</p></td>
    <td align="left"><p>更多片段</p></td>
    <td align="left"></td>
    <td align="left"><p>X</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>框架控件</p></td>
    <td align="left"><p>重试</p></td>
    <td align="left"></td>
    <td align="left"><p>X</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>框架控件</p></td>
    <td align="left"><p>Pwr</p></td>
    <td align="left"></td>
    <td align="left"><p>X</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>框架控件</p></td>
    <td align="left"><p>更多数据</p></td>
    <td align="left"></td>
    <td align="left"><p>X</p></td>
    </tr>
    <tr class="even">
    <td align="left"><p>框架控件</p></td>
    <td align="left"><p>受保护框架</p></td>
    <td align="left"></td>
    <td align="left"><p>X</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>框架控件</p></td>
    <td align="left"><p>订单</p></td>
    <td align="left"><p>X</p></td>
    <td align="left"></td>
    </tr>
    <tr class="even">
    <td align="left"><p>持续时间/ID</p></td>
    <td align="left"></td>
    <td align="left"></td>
    <td align="left"><p>X</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>地址1</p></td>
    <td align="left"></td>
    <td align="left"><p>X</p></td>
    <td align="left"></td>
    </tr>
    <tr class="even">
    <td align="left"><p>地址2</p></td>
    <td align="left"></td>
    <td align="left"><p>X</p></td>
    <td align="left"></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>地址3</p></td>
    <td align="left"></td>
    <td align="left"><p>X</p></td>
    <td align="left"></td>
    </tr>
    <tr class="even">
    <td align="left"><p>序列控件</p></td>
    <td align="left"><p>片段号</p></td>
    <td align="left"></td>
    <td align="left"><p>X</p></td>
    </tr>
    <tr class="odd">
    <td align="left"><p>序列控件</p></td>
    <td align="left"><p>序列号</p></td>
    <td align="left"></td>
    <td align="left"><p>X</p></td>
    </tr>
    </tbody>
    </table>

     

-   IHV 扩展 DLL 调用 [**Dot11ExtSendPacket**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_packet) 函数通过无线 LAN (WLAN) 适配器发送数据包。 DLL 向函数的 *hSendCompletion* 参数传递一个唯一的句柄值（用于标识数据包）。 通常，DLL 会将包含数据包的已分配缓冲区的地址传递给 *hSendCompletion* 参数。
    **注意**  仅可通过对 [**Dot11ExtSendPacket**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_packet) 函数的调用发送单播数据包。

     

-   当 WLAN 适配器发送数据包后，操作系统将调用 [*Dot11ExtIhvSendPacketCompletion*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_send_packet_completion) 函数。 操作系统将包的句柄值传递到函数的 *hSendCompletion* 参数。 此句柄值在其对 [**Dot11ExtSendPacket**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_packet)的调用中使用的值与 IHV 扩展 DLL 使用的值相同。

    调用 [*Dot11ExtIhvSendPacketCompletion*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_send_packet_completion) 时，IHV 扩展 DLL 必须释放为数据包分配的内存。

    **注意** 如果对 [*Dot11ExtIhvSendPacketCompletion*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_send_packet_completion)发出了相应的调用，则 IHV 扩展 DLL 不得释放为通过 [**Dot11ExtSendPacket**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_packet)发送的数据包分配的资源。

     

 

 
