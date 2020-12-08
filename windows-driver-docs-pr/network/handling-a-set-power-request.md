---
title: 处理设置电源请求
description: 处理设置电源请求
keywords:
- 设置-power requests WDK NDIS 中间
- 睡眠状态 WDK NDIS 中间
- 工作状态 WDK NDIS 中间
- 备用标志 WDK NDIS 中间
- 电源状态 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66618af2d4eafe6691fda2841c51167e9c7e6c3c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788359"
---
# <a name="handling-a-set-power-request"></a>处理设置电源请求





中间驱动程序必须处理请求，以设置 (的网络设备电源状态为 D0) ，并 (网络设备电源状态为 D1、D2 或 D3) 来设置工作状态的电源。 中间驱动程序还应维护电源状态变量和备用标志。 本主题将进一步讨论这些问题。

有关中间驱动程序电源管理的示例，请参阅 GitHub 上的[Windows 驱动程序示例](https://go.microsoft.com/fwlink/p/?LinkId=616507)存储库中的[NDIS MUX 中间驱动程序和通知对象](https://go.microsoft.com/fwlink/p/?LinkId=617916)驱动程序示例。

### <a name="handling-a-set-power-request-to-a-sleeping-state"></a>处理进入睡眠状态的电源请求

在以下两种情况下，中间驱动程序必须处理进入睡眠状态的电源请求：

-   NDIS 请求中间驱动程序的虚拟小型端口上部边缘进入睡眠状态。

-   中间驱动程序协议的下边缘处理在收到即插即用 (PnP) 事件通知时，基础微型端口驱动程序转换为休眠状态。

这些事件可按任意顺序发生，并且一个事件不一定会伴随另一个事件。

当中间驱动程序的虚拟小型端口上边缘收到设置进入睡眠状态的电源的请求时，处理请求的事件序列如下：

1.  NDIS 调用绑定到虚拟小型端口的每个协议驱动程序的 [*ProtocolNetPnPEvent*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_net_pnp_event) 函数。 对 *ProtocolNetPnPEvent* 的调用为休眠状态指定 **NetEventSetPower** 事件。 绑定到中间驱动程序的协议驱动程序停止发送网络数据，并对中间驱动程序虚拟小型端口发出 OID 请求。 中介驱动程序的下边缘协议可以继续发送网络数据和请求，直到 NDIS 指示基础微型端口驱动程序正在转换为休眠状态。

2.  在发出 **NetEventSetPower** 事件后，NDIS 暂停过量驱动程序和虚拟小型端口。 指定的暂停原因是转换到低功耗状态。 有关暂停虚拟小型端口的详细信息，请参阅 [暂停适配器](pausing-an-adapter.md)。

    **注意**  不能将 OID 请求发送到处于低功耗状态的虚拟小型端口，但 [oid \_ PNP \_ 集的 \_ 电源](./oid-pnp-set-power.md)除外。

     

3.  NDIS 向中间驱动程序的虚拟小型端口发出 [OID \_ PNP \_ 集 \_ 电源](./oid-pnp-set-power.md) 请求。 中间驱动程序通过返回 NDIS 状态 "成功" 来接受请求 \_ \_ 。 中间驱动程序不得将 OID \_ PNP \_ 设置 \_ 电源请求传播到基础微型端口驱动程序。 中间驱动程序完成此请求后，它不应指示收到的任何网络数据或指示状态，即使它一直接收来自基础微型端口驱动程序的网络数据和状态指示。

当中间驱动程序的协议下边缘将基础微型端口驱动程序转换为休眠状态时，用于处理该转换的事件序列如下所示：

1.  NDIS 调用中间驱动程序协议下边缘的 [*ProtocolNetPnPEvent*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_net_pnp_event) 函数。 对 *ProtocolNetPnPEvent* 的调用为休眠状态指定 **NetEventSetPower** 事件。 中间驱动程序必须停止发送网络数据，并对底层微型端口驱动程序发出 OID 请求。 如果有未完成的请求或发送，中间驱动程序应 \_ 从对 \_ *ProtocolNetPnPEvent* 的调用返回 NDIS 状态 "挂起"。 中间驱动程序调用 [**NdisCompleteNetPnPEvent**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscompletenetpnpevent) 来完成对 *ProtocolNetPnPEvent* 的调用。 中间驱动程序的协议边缘仍可以从基础微型端口驱动程序收到数据包和状态指示。 可以忽略接收的网络数据。 如果中间驱动程序的实现取决于监视基础微型端口驱动程序的状态，则仍应监视状态指示。

2.  NDIS 暂停中间驱动程序的协议边缘，然后在发出 **NetEventSetPower** 事件后暂停 underying 微型端口适配器。 指定的暂停原因是转换到低功耗状态。 有关暂停协议绑定的详细信息，请参阅 [暂停绑定](pausing-a-binding.md)。

    **注意**  不能将 OID 请求发送到低功耗状态下的基础微型端口适配器， [oid \_ PNP \_ 设置 \_ 能力](./oid-pnp-set-power.md)例外。

     

3.  NDIS 向底层微型端口驱动程序发出 [OID \_ PNP \_ 集 \_ 电源](./oid-pnp-set-power.md) 请求。 但是，如果基础微型端口驱动程序不支持电源管理，则会停止该驱动程序。 在这种情况下，即使 NDIS 暂停基础微型端口驱动程序，它也不会请求从基础微型端口驱动程序和 NIC 取消绑定中间驱动程序协议。 基础微型端口驱动程序成功处理完 OID (或微型端口驱动程序) 停止后，它不会指示任何更多网络数据或状态。

### <a name="handling-a-set-power-request-to-the-working-state"></a>处理工作状态的设置电源请求

在以下两种情况下，中间驱动程序会将已设置的电源请求处理到工作状态：

-   NDIS 请求中间驱动程序的虚拟小型端口上部边缘到工作状态。

-   当接收到即插即用 (PnP) 事件通知时，中间驱动程序协议的下边缘将处理基础微型端口驱动程序到工作状态的转换。

这些事件可按任意顺序发生，并且一个事件不一定会伴随另一个事件。

当中间驱动程序的虚拟小型端口上边缘收到设置工作状态的电源的请求时，处理请求的事件序列如下：

1.  NDIS 向中间驱动程序的虚拟小型端口发出 [OID \_ PNP \_ 集 \_ 电源](./oid-pnp-set-power.md) 。 中间驱动程序将 NDIS \_ 状态 \_ 成功返回到设置电源请求。 中间驱动程序不得将 OID \_ PNP \_ 设置 \_ 电源请求传播到基础微型端口驱动程序。

2.  NDIS 重新启动虚拟小型端口，然后在发出设置电源 OID 后重新启动过量驱动程序。 有关重新启动虚拟小型端口的详细信息，请参阅 [启动适配器](starting-an-adapter.md)。

3.  NDIS 调用过量协议驱动程序的 [*ProtocolNetPnPEvent*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_net_pnp_event) 函数。 对 *ProtocolNetPnPEvent* 的调用指定 **NetEventSetPower** 事件，以将工作状态设置 (D0) 。 绑定协议驱动程序可以开始向中间驱动程序的虚拟小型端口发送网络数据。

当中间驱动程序的协议下边缘将基础微型端口驱动程序转换为工作状态时，用于处理该转换的事件序列如下所示：

1.  如果基础微型端口驱动程序已停止，NDIS 会向底层微型端口驱动程序发出 [OID \_ PNP \_ 设置 \_ 电源](./oid-pnp-set-power.md) ，或调用其 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 处理程序。

2.  在发出 OID 后，NDIS 重新启动基础微型端口驱动程序，然后重新启动中间 NDIS 和基础微型端口适配器的协议边缘。 有关暂停协议绑定的详细信息，请参阅 [重新启动绑定](restarting-a-binding.md)。

3.  NDIS 调用中间驱动程序的 [*ProtocolNetPnPEvent*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_net_pnp_event) 函数。 对 *ProtocolNetPnPEvent* 的调用指定 **NetEventSetPower** 事件，以将工作状态设置 (D0) 。 中间驱动程序可以开始向基础微型端口驱动程序发送网络数据。

### <a name="power-states-and-the-standby-flag"></a>电源状态和备用标志

中间驱动程序应为每个虚拟微型端口实例和该驱动程序绑定到的每个基础微型端口驱动程序维护单独的电源状态变量。 中间驱动程序还应为每个虚拟小型端口维护 StandingBy 标志：

-   如果虚拟微型端口或基础微型端口驱动程序的电源状态保留 D0，则设置为 **TRUE** 。

-   如果虚拟微型端口或基础微型端口驱动程序的电源状态返回到 D0，则设置为 **FALSE** 。

**注意**  对于 MUX 中间驱动程序，可以有多个与每个虚拟小型端口关联的基础微型端口驱动程序或多个基础微型端口关联的虚拟微型端口。 任何微型端口适配器的电源状态发生变化时，所有关联的微型端口的行为也会受到影响。 此行为的影响方式是特定于实现的。 例如，在停用单个基础微型端口驱动程序时，实现负载平衡故障转移 (LBFO) 解决方案的驱动程序可能不会停用虚拟微型端口。 但是，如果任何基础微型端口驱动程序被停用，则依赖于所有基础微型端口驱动程序的驱动程序实现需要停用虚拟微型端口。

 

处理请求时，中间驱动程序应使用 StandingBy 标志和电源状态变量，如下所示：

-   此驱动程序的 [*MiniportSendNetBufferLists*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_send_net_buffer_lists) 函数应失败，除非虚拟微型端口及其基础微型端口适配器均为 D0。

-   驱动程序的 [*MiniportOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request) 函数应始终成功执行 oid \_ pnp \_ 查询 \_ 能力，以确保驱动程序接收后续 OID \_ pnp \_ 集 \_ 电源请求。

-   如果虚拟小型端口不是 D0 或 StandingBy 为 **TRUE**，则驱动程序的 [*MiniportOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)函数应失败。 否则，如果基础微型端口驱动程序不是 D0，则它应将单个请求排队。 当基础微型端口驱动程序状态变为 D0 时，应处理排队的请求。

-   仅当基础微型端口驱动程序和虚拟小型端口都为 D0 时，中间驱动程序虚拟小型端口才应报告状态。

 

