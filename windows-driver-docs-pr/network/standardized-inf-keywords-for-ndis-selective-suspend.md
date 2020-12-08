---
title: NDIS 选择性挂起的标准化 INF 关键字
description: NDIS 选择性挂起的标准化 INF 关键字
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6b34a316aec03c857f47d044ceec4152555d9c45
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839987"
---
# <a name="standardized-inf-keywords-for-ndis-selective-suspend"></a>NDIS 选择性挂起的标准化 INF 关键字


定义了以下标准化 INF 关键字，以便在微型端口驱动程序上为 NDIS 选择性挂起启用、禁用和配置参数：

[**\* SelectiveSuspend** INF 关键字](#selectivesuspend-inf-keyword)

[**\* SSIdleTimeout** INF 关键字](#ssidletimeout-inf-keyword)

[**\* SSIdleTimeoutScreenOff** INF 关键字](#ssidletimeoutscreenoff-inf-keyword)


有关标准化 INF 关键字的详细信息，请参阅 [网络设备的标准化 Inf 关键字](standardized-inf-keywords-for-network-devices.md)。

## <a name="selectivesuspend-inf-keyword"></a>\*SelectiveSuspend INF 关键字


支持 NDIS 选择性挂起的微型端口驱动程序的 INF 文件必须指定 **\* SELECTIVESUSPEND** 标准化 INF 关键字。 安装驱动程序后，管理员可以在网络适配器的 "**高级**" 属性页中更新 **\* SelectiveSuspend** 关键字值。 有关高级属性的详细信息，请参阅 [指定高级属性页的配置参数](specifying-configuration-parameters-for-the-advanced-properties-page.md)。

**注意**   在适配器的 " **高级** " 属性页中进行更改后，会自动重新启动微型端口驱动程序。

 

**\* SelectiveSuspend** INF 关键字是一个枚举关键字。 下表描述了 **\* SelectiveSuspend** inf 关键字的可能 inf 条目。 此表中的列描述了用于枚举关键字的以下属性：

<a href="" id="subkeyname"></a>SubkeyName  
必须在 INF 文件中指定的关键字的名称。 此名称还会显示在注册表中网络适配器的 **NDI \\ params \\** 键下。

<a href="" id="paramdesc"></a>ParamDesc  
与 SubkeyName 关联的显示文本。

**注意**  独立硬件供应商 (IHV) 可以定义 SubkeyName 的任何说明性文本。

 

<a href="" id="value"></a>“值”  
与列表中的每个 SubkeyName 相关联的枚举整数值。

<a href="" id="enumdesc"></a>EnumDesc  
与显示在 " **高级** " 属性页中的每个值相关联的显示文本。

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
<td align="left"><p><strong>*SelectiveSuspend</strong></p></td>
<td align="left"><p>选择性挂起</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>已禁用</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"></td>
<td align="left"><p>1 (默认值) </p></td>
<td align="left"><p>已启用</p></td>
</tr>
</tbody>
</table>

 

微型端口驱动程序必须在 **\* SelectiveSuspend** 关键字值公布其对 NDIS 选择性挂起的支持之前，检查注册表中的关键字值。 如果 **\* SelectiveSuspend** 关键字的值为零，则微型端口不得为任何选择性挂起功能公布支持。 有关详细信息，请参阅 [报告 NDIS 选择性挂起功能](reporting-ndis-selective-suspend-capabilities.md)。

## <a name="ssidletimeout-inf-keyword"></a>\*SSIdleTimeout INF 关键字


支持 NDIS 选择性挂起的微型端口驱动程序的 INF 文件应指定可选的 **\* SSIDLETIMEOUT** 标准化 INF 关键字。 此关键字指定空闲超时期限（以秒为单位）。 如果 NDIS 在网络适配器上检测不到超过 **\* SSIdleTimeout** 值的任何活动，ndis 会通过调用微型端口驱动程序的 [*MiniportIdleNotification*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification)处理程序函数来启动选择性挂起操作。

安装驱动程序后，管理员可以在网络适配器的 "**高级**" 属性页中更新 **\* SSIdleTimeout** 关键字值。 有关高级属性的详细信息，请参阅 [指定高级属性页的配置参数](specifying-configuration-parameters-for-the-advanced-properties-page.md)。

**注意**   在适配器的 "高级" 属性页中进行更改后，会自动重新启动微型端口驱动程序。

 

**\* SSIdleTimeout** INF 关键字是数字 (**Int**) 关键字。 下表描述了 **\* SSIdleTimeout** inf 关键字的可能 inf 条目。 表中的列描述 **Int** 关键字的以下属性：

<a href="" id="subkeyname"></a>SubkeyName  
必须在 INF 文件中指定的关键字的名称。 此名称还会显示在注册表中网络适配器的 **NDI \\ params \\** 键下。

<a href="" id="paramdesc"></a>ParamDesc  
与 SubkeyName 关联的显示文本。

**注意**  独立硬件供应商 (IHV) 可以定义 SubkeyName 的任何说明性文本。

 

<a href="" id="default-value"></a>默认值  
整数的默认值。

<a href="" id="minimum-value"></a>最小值  
允许用于整数的最小值。

<a href="" id="maximum-value"></a>最大值  
整数允许的最大值。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">SubkeyName</th>
<th align="left">ParamDesc</th>
<th align="left">默认值</th>
<th align="left">最小值</th>
<th align="left">最大值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>*SSIdleTimeout</strong></p></td>
<td align="left"><p>选择性挂起空闲超时（以秒为单位）</p></td>
<td align="left"><p>5</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>60</p></td>
</tr>
</tbody>
</table>

 

**注意** NDIS 读取其驱动程序支持 NDIS 选择性挂起的每个网络适配器实例的 **\* SSIDLETIMEOUT** 标准化 INF 关键字的值。 微型端口驱动程序不应读取此关键字。

 

NDIS 通过使用在 **\* SSIdleTimeout** 值的30% 范围内精确到的计时器来度量空闲超时。 例如，如果 **\* SSIdleTimeout** 值为10，则在 NDIS 首次检测到适配器处于空闲状态后，该适配器将在10到13秒之间暂停。


## <a name="ssidletimeoutscreenoff-inf-keyword"></a>\*SSIdleTimeoutScreenOff INF 关键字


支持 NDIS 选择性挂起的微型端口驱动程序的 INF 文件应指定可选的 **\* SSIDLETIMEOUTSCREENOFF** 标准化 INF 关键字。 此关键字指定空闲超时期限（以秒为单位），仅当屏幕关闭时才适用。 如果在屏幕关闭之后，NDIS 在网络适配器上检测不到超过 **\* SSIdleTimeoutScreenOff** 值的任何活动，ndis 会通过调用微型端口驱动程序的 [*MiniportIdleNotification*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_idle_notification)处理程序函数来启动选择性挂起操作。

安装驱动程序后，管理员可以在网络适配器的 "**高级**" 属性页中更新 **\* SSIdleTimeoutScreenOff** 关键字值。 有关高级属性的详细信息，请参阅 [指定高级属性页的配置参数](specifying-configuration-parameters-for-the-advanced-properties-page.md)。

**注意**   在适配器的 "高级" 属性页中进行更改后，会自动重新启动微型端口驱动程序。

 

**\* SSIdleTimeoutScreenOff** INF 关键字是数字 (**Int**) 关键字。 下表描述了 **\* SSIdleTimeoutScreenOff** inf 关键字的可能 inf 条目。 表中的列描述 **Int** 关键字的以下属性：

<a href="" id="subkeyname"></a>SubkeyName  
必须在 INF 文件中指定的关键字的名称。 此名称还会显示在注册表中网络适配器的 **NDI \\ params \\** 键下。

<a href="" id="paramdesc"></a>ParamDesc  
与 SubkeyName 关联的显示文本。

**注意**  独立硬件供应商 (IHV) 可以定义 SubkeyName 的任何说明性文本。

 

<a href="" id="default-value"></a>默认值  
整数的默认值。

<a href="" id="minimum-value"></a>最小值  
允许用于整数的最小值。

<a href="" id="maximum-value"></a>最大值  
整数允许的最大值。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">SubkeyName</th>
<th align="left">ParamDesc</th>
<th align="left">默认值</th>
<th align="left">最小值</th>
<th align="left">最大值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>*SSIdleTimeoutScreenOff</strong></p></td>
<td align="left"><p>选择性挂起空闲超时（以秒为单位）</p></td>
<td align="left"><p>3</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>60</p></td>
</tr>
</tbody>
</table>

 

**注意** NDIS 读取其驱动程序支持 NDIS 选择性挂起的每个网络适配器实例的 **\* SSIDLETIMEOUTSCREENOFF** 标准化 INF 关键字的值。 微型端口驱动程序不应读取此关键字。

**注意**  最大值仅用于测试目的。 如果值超过5，则 HLK 认证测试将显式检查并失败。

 
NDIS 通过使用在 **\* SSIdleTimeoutScreenOff** 值的30% 范围内精确到的计时器来度量空闲超时。 例如，如果 **\* SSIdleTimeoutScreenOff** 的值为5，则在 NDIS 首次检测到适配器处于空闲状态后，适配器将在5到6.5 秒之间暂停。


