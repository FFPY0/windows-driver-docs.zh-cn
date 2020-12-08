---
title: NDIS QoS 的标准化 INF 关键字
description: NDIS QoS 的标准化 INF 关键字
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e8eea8e0ebba77608c54a9b5726961f8c851a07
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803497"
---
# <a name="standardized-inf-keywords-for-ndis-qos"></a>NDIS QoS 的标准化 INF 关键字


定义了标准化的 INF 关键字，以便在微型端口驱动程序上启用或禁用 NDIS 服务 (QoS) 支持。

支持 NDIS QoS 的适配器的微型端口驱动程序的 INF 文件必须指定 **\* QOS** 标准化 INF 关键字。 安装驱动程序后，管理员可以在适配器的 "**高级**" 属性页中更新 **\* QOS** 关键字值。 有关高级属性的详细信息，请参阅 [指定高级属性页的配置参数](specifying-configuration-parameters-for-the-advanced-properties-page.md)。

**注意**   在适配器的 " **高级** " 属性页中进行更改后，会自动重新启动微型端口驱动程序。

 

**\* QOS** INF 关键字是一个枚举关键字。 下表描述了 **\* QOS** INF 关键字的可能 INF 条目。 此表中的列描述了用于枚举关键字的以下属性：

<a href="" id="subkeyname"></a>SubkeyName  
必须在 INF 文件中指定的关键字的名称。 此名称还会显示在注册表中网络适配器的 **NDI \\ params \\** 键下。

<a href="" id="paramdesc"></a>ParamDesc  
与 SubkeyName 关联的显示文本。

**注意**  独立硬件供应商 (IHV) 可以定义 SubkeyName 的任何说明性文本。

 

<a href="" id="value"></a>“值”  
与列表中的每个 SubkeyName 相关联的枚举整数值。

<a href="" id="enumdesc"></a>EnumDesc  
与菜单中显示的每个值相关联的显示文本。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">SubkeyName</th>
<th align="left">ParamDesc</th>
<th align="left">“值”</th>
<th align="left">EnumDesc</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>* QOS</strong></p></td>
<td align="left"><p>NDIS QoS</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>QoS 已禁用</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 (默认值) </p></td>
<td align="left"><p>已启用 QoS</p></td>
</tr>
</tbody>
</table>

 

当 NDIS 调用微型端口驱动程序的 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数时，驱动程序必须执行以下操作：

-   微型端口驱动程序必须注册网络适配器支持的 NDIS QoS 硬件功能。

-   微型端口驱动程序还必须读取注册表中的 **\* QOS** 关键字值，以注册适配器的 NDIS QOS 硬件功能的当前状态。

当微型端口驱动程序注册 NDIS QoS 硬件功能的当前状态时，必须遵循以下准则：

-   如果 **\* QOS** 关键字的值为1，则微型端口驱动程序必须将所有 NDIS QOS 硬件功能注册为 "当前已启用"。 驱动程序必须启用其 NDIS QoS 硬件功能，而不考虑以下各项：

    -   Windows Server 2012 和更高版本的 Windows server 上是否安装或启用了 Microsoft 数据中心桥接 (DCB) 服务器功能。 有关此服务器功能和相关组件的详细信息，请参阅 [用于数据中心桥接的 NDIS QoS 体系结构](ndis-qos-architecture-for-data-center-bridging.md)。

    -   是否在网络适配器上启用了本地数据中心桥接 Exchange (DCBX) 。 当启用此状态时，网络适配器和微型端口驱动程序可以从远程对等方收到的远程 NDIS QoS 参数解析其操作的 NDIS QoS 参数。 有关详细信息，请参阅 [管理本地 DCBX](managing-the-local-dcbx-willing-state.md)。

    有关如何注册 QoS 硬件和当前功能的详细信息，请参阅 [注册 NDIS QoS 功能](registering-ndis-qos-capabilities.md)。

    **注意**  如果当前启用了其 NDIS QoS 硬件功能，微型端口驱动程序必须始终发出 [**ndis \_ 状态 \_ qos \_ 操作 \_ 参数 \_ 更改**](./ndis-status-qos-operational-parameters-change.md) ， [**ndis \_ 状态 \_ qos \_ 远程 \_ 参数 \_ 更改**](./ndis-status-qos-remote-parameters-change.md) 状态指示。 从 Windows Server 2012 开始，这些状态指示分别报告了当前操作和远程 QoS 参数设置。 不管是否安装了 Microsoft DCB 服务器功能，这些指示都允许系统管理员查看 NDIS QoS 和 DCB 设置。 有关详细信息，请参阅 [指示 NDIS QoS 参数状态](indicating-ndis-qos-parameter-status.md)。

     

-   如果 **\* QOS** 关键字的值为零，则微型端口驱动程序必须将所有 NDIS QOS 硬件功能报告为当前禁用。 在这种情况下，操作系统不会将驱动程序配置为具有 NDIS QoS 功能。

    **注意** 如果 **\* QOS** 关键字的值为零，则驱动程序必须在网络适配器上禁用 DCB 和 DCBX。

     

-   如果注册表中不存在 **\* QOS** 关键字，则微型端口驱动程序不能报告任何 NDIS QOS 硬件功能。 在这种情况下，操作系统不会将驱动程序配置为具有 NDIS QoS 功能。

    **注意** 如果注册表中不存在 **\* QOS** 关键字，则驱动程序必须在网络适配器上禁用 DCB 和 DCBX。

     

除了 **\* QOS** 关键字，微型端口驱动程序必须读取 **\* PriorityVLANTag** 关键字。 此关键字指定是否启用网络适配器，以便为数据包优先级和虚拟 Lan (Vlan) 插入 802.1 Q 标记。

下表总结了 **\* QOS** 和 **\* PriorityVLANTag** 关键字值之间的关系。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"><em>QOS 关键字设置</th>
<th align="left"></em>PriorityVLANTag 关键字设置</th>
<th align="left">* PriorityVLANTag 设置说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">0或不存在</td>
<td align="left"><p>0</p></td>
<td align="left"><p>禁用了包优先级 & VLAN</p></td>
</tr>
<tr class="even">
<td align="left">0或不存在</td>
<td align="left"><p>1</p></td>
<td align="left"><p>启用数据包优先级</p></td>
</tr>
<tr class="odd">
<td align="left">0或不存在</td>
<td align="left"><p>2</p></td>
<td align="left"><p>已启用 VLAN</p></td>
</tr>
<tr class="even">
<td align="left">0或不存在</td>
<td align="left"><p>3 (默认值) </p></td>
<td align="left"><p>已启用数据包优先级和 VLAN</p></td>
</tr>
<tr class="odd">
<td align="left">1</td>
<td align="left"><p>0</p></td>
<td align="left"><p>启用数据包优先级</p></td>
</tr>
<tr class="even">
<td align="left">1</td>
<td align="left"><p>1</p></td>
<td align="left"><p>启用数据包优先级</p></td>
</tr>
<tr class="odd">
<td align="left">1</td>
<td align="left"><p>2</p></td>
<td align="left"><p>已启用数据包优先级和 VLAN</p></td>
</tr>
<tr class="even">
<td align="left">1</td>
<td align="left"><p>3 (默认值) </p></td>
<td align="left"><p>已启用数据包优先级和 VLAN</p></td>
</tr>
</tbody>
</table>

 

有关 **\* PriorityVLANTag** 关键字的详细信息，请参阅 [枚举关键字](enumeration-keywords.md)。

有关标准化 INF 关键字的详细信息，请参阅 [网络设备的标准化 Inf 关键字](standardized-inf-keywords-for-network-devices.md)。

有关如何注册 NDIS QoS 功能的详细信息，请参阅 [注册 Ndis Qos 功能](registering-ndis-qos-capabilities.md)。

 

