---
title: OID_WWAN_CONNECT
description: OID_WWAN_CONNECT 激活或停用特定的数据包上下文并读取上下文的激活状态。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_WWAN_CONNECT 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 5694b161be1c057629e0307dcc0f047cef6a098f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797981"
---
# <a name="oid_wwan_connect"></a>OID \_ WWAN \_ 连接


OID \_ WWAN \_ CONNECT 激活或停用特定的数据包上下文并读取上下文的激活状态。

微型端口驱动程序必须异步处理集和查询请求，最初 \_ 返回 \_ \_ 原始请求所需的 ndis 状态指示，稍后发送 [**ndis \_ 状态 \_ WWAN \_ 上下文 \_ 状态**](ndis-status-wwan-context-state.md) 通知，其中包含 [**一个 \_ ndis \_ WWAN \_ 上下文**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_context_state) 状态，该结构指示在 MB 设备上 (PDP) 上下文状态，而不考虑完成集或查询请求。

调用方请求将数据包数据协议设置为 MB 设备 (PDP) 上下文状态，并使用相应的信息为微型端口驱动程序提供 [**NDIS \_ WWAN \_ 设置 \_ 上下文 \_ 状态**](/windows-hardware/drivers/ddi/ndiswwan/ns-ndiswwan-_ndis_wwan_set_context_state) 结构。

<a name="remarks"></a>备注
-------

有关使用此 OID 的详细信息，请参阅 [WWAN 数据包上下文管理](./mb-packet-context-management.md)。

此对象激活或停用特定的数据包上下文并读取上下文的激活状态。 当激活状态发生变化时，微型端口驱动程序必须发送相应的事件通知。

仅当微型端口驱动程序处于 **WwanRegisterStateHome**、 **WwanRegisterStatePartner** 或 **WwanRegisterStateRoaming** 的注册状态时，才会调用此对象。 当数据包服务处于活动状态时，该设备还必须处于 **WwanPacketServiceStateAttached** 的附加状态。

此对象支持 set 和 query 操作。

-   处理集请求需要网络访问，但不需要访问 SIM。

-   处理查询请求不需要访问网络或 SIM。

此 OID 的数据结构为 NDIS \_ WWAN \_ 集 \_ 上下文 \_ 状态。 \_ \_ \_ \_ 对于 set 和 query 请求，微型端口驱动程序会发出 "NDIS 状态" WWAN 上下文状态的状态指示。

在此版本的驱动程序模型中，微型端口驱动程序仅在 MB 服务指示的情况下尝试上下文激活。  (微型端口驱动程序可能会激活在更高版本中由网络启动的上下文。 ) 微型端口驱动程序甚至不得自动激活上下文，即使在失去注册或发出信号后也是如此。 如果激活请求中未提供访问字符串，则微型端口驱动程序不应尝试提供默认字符串。 相反，它必须继续使用空白访问字符串激活上下文。

另一方面，小型端口驱动程序可以按 MB 服务的指示停用上下文。 如果网络连接已丢失，超过了信号暂时丢失的阈值，或者作为正常关机或状态清理的一部分，则可能会发生这种情况。

由于此版本中仅支持一个激活的上下文，因此激活或停用特定的上下文数量，以设置或撕裂第2层连接。

在设置请求时，MB 服务 furnishes WWAN **ConnectionId** **ActivationCommand** \_ 上下文 \_ 状态数据结构中的 ConnectionId 和 ActivationCommand 参数。 基于 **ActivationCommand** 参数值 *WwanActivationCommandActivate* 或 *WwanActivationCommandDeactivate*，它指示微型端口驱动程序激活或停用 **ConnectionId** 标识的数据包上下文。

-   如果服务或订阅需要激活，微型端口驱动程序应返回错误代码 WWAN \_ 状态 \_ 服务 " \_ 未 \_ 激活"。 在激活服务或订阅之前，可能不会发生 PDP 激活。 所有紧急服务都可能受设备和操作员提供的支持的限制。 操作系统可能会调用 OID \_ WWAN \_ 服务激活， \_ 以响应此错误代码。

-   如果微型端口驱动程序在当前激活其他数据包上下文时接收上下文激活请求，则将返回错误代码 "WWAN \_ 状态 \_ 最大 \_ 激活 \_ 上下文"。

-   如果微型端口驱动程序收到上下文停用请求，但 **ConnectionId** 标识的上下文当前未激活，它将返回错误代码 "WWAN \_ 状态 \_ 上下文 \_ 未 \_ 激活"。

微型端口驱动程序使用以下逻辑来确定设置请求中 AccessString、用户名和密码设置的有效性：

-   如果 **ActivationCommand** 为 *WwanActivationCommandDeactivate*，则微型端口驱动程序应忽略这三个参数的设置。 其余情况下，仅在 **ActivationCommand** 为 *WwanActivationCommandActivate* 时才考虑这种情况。

上下文激活会在用户登录和注销期间保持。 它不是每个登录用户。

在查询请求中，MB 服务使用此对象来找出激活状态。

对于对查询请求的响应，微型端口驱动程序将发送 NDIS \_ 状态 \_ WWAN \_ 上下文 \_ 状态通知。

**重要提示**  纪录

 

在极少数情况下，在特定情况下，Windows 7 上的 MB 服务可能会尝试自动连接，然后才能为预先存在的连接确定连接到 Internet 的连接，或者在暂时中断之前现有连接的 Internet 连接过程中。 这可能会导致同时出现 MB 和 WLAN/以太网连接。 例如，当同时尝试使用 MB 和其他连接并且网络列表管理器服务仍尝试使用主动和被动方法确定其他连接的 Internet 连接时，系统启动期间可能会发生这种情况。 这也可能是由于网络基础结构（如企业代理服务器或 ISP 网络）的临时中断引起的。 因此，MB 服务可能会尝试自动连接到 internet，而不管是否选择了 "如果没有可用的备用 Internet 连接，则自动连接" 选项。

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
<td><p>在 windows 7 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[WWAN 数据包上下文管理](./mb-packet-context-management.md)

 

