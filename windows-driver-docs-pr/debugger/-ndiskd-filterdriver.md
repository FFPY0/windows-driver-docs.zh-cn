---
title: ndiskd.filterdriver
description: Ndiskd. filterdriver 扩展显示有关 NDIS 筛选器驱动程序的信息。 如果运行不带任何参数的扩展，ndiskd 将显示所有筛选器驱动程序的列表。
keywords:
- ndiskd filterdriver Windows 调试
ms.date: 06/15/2020
topic_type:
- apiref
api_name:
- ndiskd.filterdriver
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3fa8a1c26da230143c654abaa6a23ecd3455fc30
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832549"
---
# <a name="ndiskdfilterdriver"></a>!ndiskd.filterdriver

**！ Ndiskd filterdriver** 扩展显示有关 NDIS 筛选器驱动程序的信息。 如果运行不带参数的扩展，！ ndiskd 将显示所有筛选器驱动程序的列表。

```console
!ndiskd.filterdriver -handle <x> [-filters] [-handlers] 
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters

<span id="_______-handle______"></span><span id="_______-HANDLE______"></span>*-handle*   
NDIS 筛选器驱动程序的可选句柄。

<span id="_______-filters______"></span><span id="_______-FILTERS______"></span>*-筛选器*   
显示此驱动程序的筛选器的实例。

<span id="_______-handlers______"></span><span id="_______-HANDLERS______"></span>*-处理程序*   
显示此驱动程序的筛选器处理程序。

### <a name="dll"></a>DLL

Ndiskd.dll

### <a name="examples"></a>示例

不带参数的 **ndiskd！ filterdriver** ，以查看系统上所有筛选器驱动程序的列表。 在下面的示例中，查找虚拟 WiFi 筛选器驱动程序，该驱动程序的句柄为 ffffbc064cc83be0。

```console
0: kd> !ndiskd.filterdriver
    ffffbc064ccd4900 - QoS Packet Scheduler
    ffffbc064cc83be0 - Virtual WiFi Filter Driver
    ffffbc064cb91a10 - WFP vSwitch Layers LightWeight Filter
    ffffbc064cb8fd70 - WFP Native MAC Layer LightWeight Filter
    ffffbc064cb59b00 - WFP 802.3 MAC Layer LightWeight Filter
```

通过单击上一个示例中的筛选器驱动程序句柄，或使用它在命令窗口中输入 **！ ndiskd** 命令，你可以获取有关该筛选器驱动程序的更多详细信息。 例如，在这种情况下，此筛选器驱动程序没有筛选器模块。

```console
0: kd> !ndiskd.filterdriver ffffbc064cc83be0


FILTER DRIVER

    Virtual WiFi Filter Driver

    Ndis handle        ffffbc064cc83be0
    Driver context     ffffbc064cc8e9d0
    Ndis API version   v6.50
    Driver version     v1.0
    Driver object      ffffbc064cc8e9d0
    Driver image       vwififlt.sys

    Bind flags         Optional, Modifying
    Class              [Zero-length string]
    References         1


FILTER MODULES

    Filter module                                                               
    [No filter modules were found]


HANDLERS

    Filter handler                         Function pointer   Symbol (if available)
    SetOptionsHandler                      [None]
    SetFilterModuleOptionsHandler          [None]
    AttachHandler                          fffff80787d83b60  bp
    DetachHandler                          fffff80787d84800  bp
    RestartHandler                         fffff80787d86e20  bp
    PauseHandler                           fffff80787d863e0  bp
    SendNetBufferListsHandler              fffff80787d814d0  bp
    SendNetBufferListsCompleteHandler      fffff80787d81940  bp
    CancelSendNetBufferListsHandler        fffff80787d842f0  bp
    ReceiveNetBufferListsHandler           fffff80787d817e0  bp
    ReturnNetBufferListsHandler            fffff80787d81a80  bp
    OidRequestHandler                      fffff80787d85ae0  bp
    OidRequestCompleteHandler              fffff80787d85fd0  bp
    DirectOidRequestHandler                fffff80787d84af0  bp
    DirectOidRequestCompleteHandler        fffff80787d84e80  bp
    CancelDirectOidRequestHandler          fffff80787d841d0  bp
    DevicePnPEventNotifyHandler            fffff80787d849e0  bp
    NetPnPEventHandler                     fffff80787d85a40  bp
    StatusHandler                          fffff80787d877c0  bp
```

## <a name="see-also"></a>请参阅

[网络驱动程序设计指南](../network/index.md)

[Windows Vista 和更高版本的网络引用](/windows-hardware/drivers/ddi/_netvista/)

[调试网络堆栈](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 扩展 ( # A0)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)
