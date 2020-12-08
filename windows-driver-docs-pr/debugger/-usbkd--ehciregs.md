---
title: usbkd._ehciregs
description: Usbkd._ehciregs 命令显示 USB EHCI 主机控制器的操作端口和根集线器端口状态寄存器。
keywords:
- usbkd._ehciregs Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- usbkd._ehciregs
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c92b904165547bccb736cc562ee45c4d99531773
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802043"
---
# <a name="usbkd_ehciregs"></a>！ usbkd。 \_ehciregs


**！ Usbkd。 \_ehciregs** 命令显示 USB EHCI 主机控制器的操作端口和根集线器端口状态寄存器。

```dbgcmd
!usbkd._ehciregs StructAddr[, NumPorts]
```

## <a name="span-idddk__devobj_dbgspanspan-idddk__devobj_dbgspanparameters"></a><span id="ddk__devobj_dbg"></span><span id="DDK__DEVOBJ_DBG"></span>参数


<span id="_______StructAddr______"></span><span id="_______structaddr______"></span><span id="_______STRUCTADDR______"></span>*StructAddr*   
Usbehci 的地址 **！ \_HC \_ 操作 \_ 寄存器** 结构。 查找 usbehci 的地址 **！ \_HC \_ 操作 \_ 寄存器** 结构，请使用 [**！ usbkd. usbhcdlist**](-usbkd-usbhcdlist.md)。

<span id="_______NumPorts______"></span><span id="_______numports______"></span><span id="_______NUMPORTS______"></span>*NumPorts*   
要显示的根集线器端口状态寄存器的数目。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


Usbkd.dll

<a name="examples"></a>示例
--------

下面是获取 usbehci 的地址的一种方法 **！ \_HC \_ 操作 \_ 寄存器** 结构。 首先输入 [**！ usbkd. usbhcdlist**](-usbkd-usbhcdlist.md)。

```dbgcmd
0: kd> !usbkd.usbhcdlist
MINIPORT List @ fffff80001e5bbd0

## List of EHCI controllers

!drvobj ffffe00001fd33a0 dt USBPORT!_USBPORT_MINIPORT_DRIVER ...
...
02. Xxxx Corporation PCI: VendorID Xxxx DeviceID Xxxx RevisionId 0002
    !devobj ffffe00001ca1050
    !ehci_info ffffe00001ca11a0
    Operational Registers ffffd000228bf020
```

在上面的输出中， ` ffffd000228bf020` 是 **\_ HC \_ 操作 \_ 寄存器** 结构的地址。

现在，将结构地址传递给 **！ \_ehciregs**。 在此示例中，第二个参数将显示限制为两个根集线器端口状态寄存器。

```dbgcmd
0: kd> !usbkd._ehciregs ffffd000228bf020, 2
*(ehci)HC_OPERATIONAL_REGISTER ffffd000228bf020
    USBCMD 00010001
    .HostControllerRun: 1
    .HostControllerReset: 0
    .FrameListSize: 0
    .PeriodicScheduleEnable: 0
    .AsyncScheduleEnable: 0
    .IntOnAsyncAdvanceDoorbell: 0
    .HostControllerLightReset: 0
    .InterruptThreshold: 1
    .ParkModeEnable: 0
    .ParkModeCount: 0

    USBSTS 00002008
    .UsbInterrupt: 0
    .UsbError: 0
    .PortChangeDetect: 0
    .FrameListRollover: 1
    .HostSystemError: 0
    .IntOnAsyncAdvance: 0
    ----
    .HcHalted: 0
    .Reclimation: 1
    .PeriodicScheduleStatus: 0
    .AsyncScheduleStatus: 0

    USBINTR 0000003f
    .UsbInterrupt: 1
    .UsbError: 1
    .PortChangeDetect: 1
    .FrameListRollover: 1
    .HostSystemError: 1
    .IntOnAsyncAdvance: 1
    PeriodicListBase dec8e000
    AsyncListAddr dec91000
    PortSC[0] 00001000
        PortConnect x0
        PortConnectChange x0
        PortEnable x0
        PortEnableChange x0
        OvercurrentActive x0
        OvercurrentChange x0
        ForcePortResume x0
        PortSuspend x0
        PortReset x0
        HighSpeedDevice x0
        LineStatus x0
        PortPower x1
        PortOwnedByCC x0
        PortIndicator x0
        PortTestControl x0
        WakeOnConnect x0
        WakeOnDisconnect x0
        WakeOnOvercurrent x0
    PortSC[1] 00001000
        PortConnect x0
        PortConnectChange x0
        PortEnable x0
        PortEnableChange x0
        OvercurrentActive x0
        OvercurrentChange x0
        ForcePortResume x0
        PortSuspend x0
        PortReset x0
        HighSpeedDevice x0
        LineStatus x0
        PortPower x1
        PortOwnedByCC x0
        PortIndicator x0
        PortTestControl x0
        WakeOnConnect x0
        WakeOnDisconnect x0
```

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[USB 2.0 调试器扩展](usb-2-0-extensions.md)

[ (USB) 驱动程序的通用串行总线](../usbcon/index.md)

 

