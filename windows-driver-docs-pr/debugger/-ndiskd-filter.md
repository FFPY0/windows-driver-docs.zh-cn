---
title: ndiskd 筛选器
description: Ndiskd 扩展显示有关 NDIS 轻型筛选器 (LWF) 的信息。 如果运行不带任何参数的扩展，ndiskd 将显示所有 LWFs 的列表。
keywords:
- ndiskd Windows 调试
ms.date: 06/15/2020
topic_type:
- apiref
api_name:
- ndiskd.filter
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: bb405b8ef1c58ecac126f01c39cee30d451a536e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796325"
---
# <a name="ndiskdfilter"></a>!ndiskd.filter

**！ Ndiskd** 扩展显示有关 NDIS 轻型筛选器 (LWF) 的信息。 如果运行不带参数的扩展，！ ndiskd 将显示所有 LWFs 的列表。

```console
!ndiskd.filter [-handle <x>] [-findname <any>] [-handlers]
```

## <a name="parameters"></a>参数

<span id="_______-handle______"></span><span id="_______-HANDLE______"></span>*-handle*   
NDIS 轻型筛选器的可选句柄。

<span id="_______-findname______"></span><span id="_______-FINDNAME______"></span>*-system.windows.frameworkelement.findname*   
按名称前缀筛选 LWFs。

<span id="_______-handlers______"></span><span id="_______-HANDLERS______"></span>*-处理程序*   
显示此 LWF 的筛选器处理程序。

### <a name="dll"></a>DLL

Ndiskd.dll

### <a name="examples"></a>示例

输入不带参数的 **！ ndiskd** 命令以获取所有筛选器的列表。 在此示例中，查找 ffff8083e14e8460 句柄。 请注意，此句柄用于筛选器本身，并嵌套在其关联的筛选器 *驱动程序*（QoS 数据包计划程序）之下。

```console
3: kd> !ndiskd.filter
ffff8083e1a7fd90 - QoS Packet Scheduler
  Filter ffff8083e14e8460, Miniport ffff8083e0f501a0 - Microsoft Kernel Debug Network Adapter
ffff8083e1a96b80 - Virtual WiFi Filter Driver
ffff8083e19c4b70 - WFP vSwitch Layers LightWeight Filter
ffff8083e19a6ad0 - WFP Native MAC Layer LightWeight Filter
  Filter ffff8083e43df8f0, Miniport ffff8083e0f501a0 - Microsoft Kernel Debug Network Adapter
ffff8083e19a6d70 - WFP 802.3 MAC Layer LightWeight Filter
  Filter ffff8083e0d89c70, Miniport ffff8083e0f501a0 - Microsoft Kernel Debug Network Adapter
```

通过使用此筛选器句柄，我们现在可以看到有关它的更详细信息，如 it 状态、更高的筛选器句柄和更低的筛选器句柄。

```console
3: kd> !ndiskd.filter ffff8083e14e8460


FILTER

    Microsoft Kernel Debug Network Adapter-QoS Packet Scheduler-0000

    Ndis handle        ffff8083e14e8460
    Filter driver      ffff8083e1a7fd90 - QoS Packet Scheduler
    Module context     ffff8083e26953e0
    Miniport           ffff8083e0f501a0 - Microsoft Kernel Debug Network Adapter
    Network interface  ffff8083e200f010

    State              Running
    Datapath           Send only
    References         1
    Flags              RUNNING
    More flags         OID_TOP

    Higher filter      ffff8083e0d89c70 - Microsoft Kernel Debug Network Adapter-WFP 802.3 MAC Layer LightWeight Filter-0000
    Lower filter       ffff8083e43df8f0 - Microsoft Kernel Debug Network Adapter-WFP Native MAC Layer LightWeight Filter-0000

    Driver handlers
```

## <a name="see-also"></a>请参阅

[网络驱动程序设计指南](../network/index.md)

[Windows Vista 和更高版本的网络引用](/windows-hardware/drivers/ddi/_netvista/)

[调试网络堆栈](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 扩展 ( # A0)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)
