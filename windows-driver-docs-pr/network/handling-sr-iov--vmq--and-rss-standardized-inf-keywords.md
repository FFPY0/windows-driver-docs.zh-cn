---
title: 处理 SR-IOV、VMQ 和 RSS 标准化 INF 关键字
description: 处理 SR-IOV、VMQ 和 RSS 标准化 INF 关键字
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a12dafc3e461183a595690ef1dd827f3aeadc374
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794645"
---
# <a name="handling-sr-iov-vmq-and-rss-standardized-inf-keywords"></a>处理 SR-IOV、VMQ 和 RSS 标准化 INF 关键字


支持单个根 i/o 虚拟化的网络适配器 (SR-IOV) 、虚拟机队列 (VMQ) 和接收方缩放 (RSS) 可通过以下方式实现这些接口的使用：

-   SR-IOV 和 VMQ 可以单独启用或同时启用。

-   启用 SR-IOV 或 VMQ 后，无法在网络适配器上启用 RSS。

操作系统可通过以下方式使用 SR-IOV、VMQ 或 RSS 接口：

-   将网络适配器绑定到 TCP/IP 堆栈后，操作将启用 RSS 功能的使用。

-   将网络适配器绑定到 Hyper-v 可扩展交换机驱动程序堆栈后，操作系统将支持使用 SR-IOV 或 VMQ 功能。

    有关 Hyper-v 可扩展交换机的详细信息，请参阅 [Hyper-v 可扩展交换机](hyper-v-extensible-switch.md)。

如果网络适配器未绑定到 TCP/IP 堆栈和 Hyper-v 可扩展交换机驱动程序堆栈，则会停止并重新初始化微型端口驱动程序。 因此，此类网络适配器无法自动在 RSS、VMQ 和 SR-IOV 之间切换。

当 NDIS 调用 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数时，微型端口驱动程序会在将其当前启用的 SR-IOV、VMQ 或 RSS 功能报告给 NDIS 之前，执行以下步骤：

1.  微型端口驱动程序在将其当前启用的功能报告给 NDIS 之前，读取 **\* SriovPreferred** 关键字。

    如果 **\* SriovPreferred** 关键字的值为 one，则会为 sr-iov 首选项配置微型端口驱动程序。

2.  微型端口驱动程序在将其当前启用的功能报告给 NDIS 之前，读取 **\* RssOrVmqPreference** 关键字。

    如果 **\* RssOrVmqPreference** 关键字的值为 one，则会为 VMQ 首选项配置微型端口驱动程序。

    如果 **\* RssOrVmqPreference** 关键字的值为零，或者关键字不存在，则为 RSS 首选项配置微型端口驱动程序。

3.  如果为 SR-IOV 首选项配置微型端口驱动程序，则必须读取 **\* SRIOV** 关键字，以确定网络适配器上是否已启用 sr-iov。 如果将关键字设置为 one，则驱动程序将报告当前启用的 SR-IOV 设置。

    有关微型端口驱动程序如何报告 SR-IOV 设置的详细信息，请参阅 [确定 Sr-iov 功能](determining-sr-iov-capabilities.md)。

    有关 SR-IOV 关键字的详细信息，请参阅 [sr-iov 的标准化 INF 关键字](standardized-inf-keywords-for-sr-iov.md)。

    **注意**  如果为 SR-IOV 首选项配置微型端口驱动程序，则不能读取任何 RSS 标准化关键字。 但是，驱动程序必须读取 VMQ **\* VMQVlanFiltering** 标准化关键字。 此关键字指定是否启用微型端口驱动程序，以便使用 media access control (MAC) 标头中的虚拟 VLAN (VLAN) 标识符来筛选网络数据包。 微型端口驱动程序通过在 \_ \_ \_ \_ \_ \_ \_ [**ndis \_ 接收 \_ 筛选器 \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_receive_filter_capabilities)结构的 **SupportedMacHeaderFields** 成员中设置 "支持 ndis 接收筛选器 MAC 标头 VLAN ID" 标志来报告此功能。 有关 **\* VMQVlanFiltering** 标准化关键字的详细信息，请参阅 [VMQ 的标准化 INF 关键字](standardized-inf-keywords-for-vmq.md)。

     

4.  如果为 VMQ 首选项配置微型端口驱动程序，则必须读取 **\* vmq** 关键字，以确定网络适配器上是否已启用 vmq。 如果将关键字设置为 one，则驱动程序将报告当前启用的 VMQ 设置。 有关微型端口驱动程序如何报告 VMQ 设置的详细信息，请参阅 [确定网络适配器的 Vmq 功能](determining-the-vmq-capabilities-of-a-network-adapter.md)。

    有关 VMQ 关键字的详细信息，请参阅 [vmq 的标准化 INF 关键字](standardized-inf-keywords-for-vmq.md)。

    **注意**  如果为 VMQ 首选项配置微型端口驱动程序，则不能读取任何 RSS 或 SR-IOV 标准化关键字。

     

5.  如果为 RSS 首选项配置微型端口驱动程序，则必须阅读 **\* rss** 关键字，以确定是否在网络适配器上启用了 rss。 如果将关键字设置为 one，则驱动程序将报告当前启用的 RSS 设置。 有关微型端口驱动程序如何报告 RSS 设置的详细信息，请参阅 [Rss 配置](rss-configuration.md)。

    有关 RSS 关键字的详细信息，请参阅 [rss 的标准化 INF 关键字](standardized-inf-keywords-for-rss.md)。

    **注意**  如果为 RSS 首选项配置微型端口驱动程序，则它不能读取任何 VMQ 或 SR-IOV 标准化关键字。

     

下表介绍了微型端口驱动程序如何确定 SR-IOV、VMQ 或 RSS 首选项，以便在网络适配器中启用正确的接口。

<table style="width:100%;">
<colgroup>
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><em>SriovPreferred</th>
<th align="left"></em>RssOrVmqPreference</th>
<th align="left"><em>SRIOV</th>
<th align="left"></em>VMQ</th>
<th align="left">* RSS</th>
<th align="left">启用的界面</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>不适用</p></td>
<td align="left"><p>SR-IOV 和 VMQ</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>不适用</p></td>
<td align="left"><p>VMQ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>1、0或不存在于注册表中</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>不可用</p></td>
<td align="left"><p>None</p></td>
</tr>
<tr class="even">
<td align="left"><p>0，或在注册表中不存在</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>不适用</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>不适用</p></td>
<td align="left"><p>VMQ</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0，或在注册表中不存在</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>不适用</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>不可用</p></td>
<td align="left"><p>None</p></td>
</tr>
<tr class="even">
<td align="left"><p>0，或在注册表中不存在</p></td>
<td align="left"><p>0，或在注册表中不存在</p></td>
<td align="left"><p>空值</p></td>
<td align="left"><p>空值</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>RSS</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0，或在注册表中不存在</p></td>
<td align="left"><p>0，或在注册表中不存在</p></td>
<td align="left"><p>空值</p></td>
<td align="left"><p>空值</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>无</p></td>
</tr>
</tbody>
</table>

 

**注意**  当 SR-IOV 和 VMQ 接口都已启用时，将使用连接到 PCI Express (PCIe) 物理 (功能的 SR-IOV 非默认虚拟端口 (VPorts) ，而不是对 VMQ 接口使用 VM 队列。 有关详细信息，请参阅 [非默认虚拟端口和 VMQ](nondefault-virtual-ports-and-vmq.md)。

 

微型端口驱动程序必须公布当前启用的接口的功能。 例如，如果启用了 SR-IOV，则微型端口驱动程序必须播发 SR-IOV 功能，但不能对 VMQ 或 RSS 的功能进行播发。 但是，无论在网络适配器上启用哪个接口，微型端口驱动程序必须始终报告完整的 RSS、VMQ 和 SR-IOV 硬件功能。

**注意**  VMQ 和 SR-IOV 接口使用通过 VM 队列或 SR-IOV 虚拟端口接收筛选 (VPorts) 。 因此，当其中一个接口启用时，某些接收筛选功能需要相同或不同的设置。 有关如何报告 SR-IOV 接口的接收筛选功能的详细信息，请参阅 [确定接收筛选功能](determining-receive-filtering-capabilities.md)。 有关如何为 VMQ 接口报告接收筛选功能的详细信息，请参阅 [确定网络适配器的 Vmq 功能](determining-the-vmq-capabilities-of-a-network-adapter.md)。

 

 

