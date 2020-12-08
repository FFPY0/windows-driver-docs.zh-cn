---
title: ndiskd.ndisevent
description: ！ Ndiskd ndisevent 扩展显示 NDIS 调试事件日志。
keywords:
- ndiskd ndisevent Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ndiskd.ndisevent
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 86fb6b2279ec4523d31118fa42dfcb36cd1bd715
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805829"
---
# <a name="ndiskdndisevent"></a>!ndiskd.ndisevent

**注意**  第三方网络驱动程序开发人员不需要手动使用此扩展命令。 您可以运行它来查看它所显示的信息，但不能重复使用它在您的驱动程序中提供的详细信息。

**！ Ndiskd ndisevent** 扩展显示 NDIS 调试事件日志。

```console
!ndiskd.ndisevent -handle <x> [-tagtype <str>]
```

## <a name="parameters"></a>参数

<span id="_______-handle______"></span><span id="_______-HANDLE______"></span>*-handle*   
必需。 事件日志的句柄。

<span id="_______-tagtype______"></span><span id="_______-TAGTYPE______"></span>*-tagtype*   
标记的枚举类型。

### <a name="dll"></a>DLL

Ndiskd.dll

### <a name="examples"></a>示例

若要查看网络适配器的事件日志输出，！ ndiskd 在 [**！ ndiskd**](-ndiskd-netadapter.md) 输出的 State 节中提供了一个指向它的链接。 这比从微型端口块查找事件日志句柄并使用它来运行 **！ ndiskd. ndisevent** 扩展的手动方法更容易。

首先，输入不带参数的 **！ ndiskd** 命令，以查看系统上的网络适配器和微型端口驱动程序列表。 在以下示例中，查找 Marvell AVASTAR 无线-AC 网络控制器 ffffc804b9e6f1a0 的句柄。

```console
1: kd> !ndiskd.netadapter
    Driver             NetAdapter          Name                                 
    ffffc804af2e3710   ffffc804b9e6f1a0    Marvell AVASTAR Wireless-AC Network Controller
    ffffc804b99b9020   ffffc804b9c301a0    WAN Miniport (Network Monitor)
    ffffc804b99b9020   ffffc804b9c2a1a0    WAN Miniport (IPv6)
    ffffc804b99b9020   ffffc804b8a8a1a0    WAN Miniport (IP)
    ffffc804ae9d7020   ffffc804b9ceb1a0    WAN Miniport (PPPOE)
    ffffc804b9ca5900   ffffc804b9e601a0    WAN Miniport (PPTP)
    ffffc804b99dc720   ffffc804b99b01a0    WAN Miniport (L2TP)
    ffffc804b86581b0   ffffc804b9c6c1a0    WAN Miniport (IKEv2)
    ffffc804ad4a7250   ffffc804b99651a0    WAN Miniport (SSTP)
    ffffc804b11c4020   ffffc804b85821a0    Microsoft ISATAP Adapter
    ffffc804b11c4020   ffffc804b71731a0    Microsoft ISATAP Adapter #2
    ffffc804ad725020   ffffc804b05e71a0    Surface Ethernet Adapter #2
    ffffc804b0bf0020   ffffc804b0c011a0    Bluetooth Device (Personal Area Network)
    ffffc804aef695e0   ffffc804aed331a0    TAP-Windows Adapter V9
```

现在，单击该 Get-netadapter 的链接，或输入 **！ ndiskd** 命令查看其详细信息。 在 "状态" 部分中，查找 "设备 PnP" 字段右侧的 "显示状态历史记录" 链接。

```console
1: kd> !ndiskd.netadapter ffffc804b9e6f1a0


MINIPORT

    Marvell AVASTAR Wireless-AC Network Controller

    Ndis handle        ffffc804b9e6f1a0
    Ndis API version   v6.50
    Adapter context    ffffc804af3b1100
    Driver             ffffc804af2e3710 - mrvlpcie8897  v1.0
    Network interface  ffffc804aea60a20

    Media type         802.3
    Physical medium    NdisPhysicalMediumUnspecified
    Device instance    PCI\VEN_11AB&DEV_2B38&SUBSYS_045E0001&REV_00\4&379f07b2&0&00E0
    Device object      ffffc804b9e6f050    More information
    MAC address        c0-33-5e-13-22-f7


STATE

    Miniport           INITIALIZING
    Device PnP         ADDED               Show state history
    Datapath           Normal
    Operational status DOWN
    Operational flags  [No flags set]
    Admin status       ADMIN_UP
    Media              MediaConnectUnknown
    Power              D0
    References         1                   Show detail
    Total resets       0
    Pending OID        None
    Flags              IN_INITIALIZE, NOT_BUS_MASTER, DEFAULT_PORT_ACTIVATED,
                       NOT_SUPPORTS_MEDIA_SENSE, DOES_LOOPBACK, MEDIA_CONNECTED
    PnP flags          PM_SUPPORTED, RECEIVED_START, HARDWARE_DEVICE


WDI

    This system supports WDI.
    Learn more about the associated WDI state


BINDINGS

    Protocol list      Driver              Open               Context           
    No protocols are bound to this miniport

    Filter list        Driver              Module             Context           
    No filters are bound to this miniport



MORE INFORMATION

    Driver handlers                        Task offloads
    Power management                       PM protocol offloads
    Pending OIDs                           Timers
    Pending NBLs                           Receive side throttling
    Wake-on-LAN (WoL)                      Packet filter
    Receive queues                         Receive filtering
    RSS                                    NIC switch
    Hardware resources                     Selective suspend
    NDIS ports                             WMI guids
    Diagnostic log
```

现在，你可以单击 "显示状态历史记录" 链接或使用网络适配器的句柄来输入 **！ ndiskd** 命令，该命令将显示此小型小型端口驱动程序的 PnP 事件日志。

```console
1: kd> !ndiskd.netadapter ffffc804b9e6f1a0 -log


MINIPORT PM & PNP EVENTS

    Event              Timestamp           (most recent event at bottom)        
    DeviceAdded
                       13 ms later
    DeviceStart
                       Mon Mar 20 21:27:07.106 2017 (UTC - 7:00) Now?

    Set a breakpoint on the next event
```

## <a name="see-also"></a>请参阅

[网络驱动程序设计指南](../network/index.md)

[Windows Vista 和更高版本的网络引用](/windows-hardware/drivers/ddi/_netvista/)

[调试网络堆栈](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 扩展 ( # A0)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[**!ndiskd.netadapter**](-ndiskd-netadapter.md)
