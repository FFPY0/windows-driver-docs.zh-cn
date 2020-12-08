---
title: fxdevice
description: Fxdevice 扩展显示有关) 已注册设备的所有电源管理框架 (的摘要信息。 此命令只能在内核模式调试过程中使用。
keywords:
- fxdevice Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- fxdevice
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: aa8aee24e9d6b9c0f703a1b324b6a4ef09f25150
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824789"
---
# <a name="fxdevice"></a>!fxdevice


！ Fxdevice extension 显示有关所有电源管理框架 (PoFx) 注册设备的摘要信息。 此命令只能在内核模式调试过程中使用。

有关 PoFX 的详细信息，请参阅 [电源管理框架概述](../kernel/overview-of-the-power-management-framework.md)。

语法

```dbgcmd
!fxdevice[<FxDevice Address>]
```

## <a name="span-idddk__thread_dbgspanspan-idddk__thread_dbgspanparameters"></a><span id="ddk__thread_dbg"></span><span id="DDK__THREAD_DBG"></span>参数


<span id="___________FxDevice__Address_______"></span><span id="___________fxdevice__address_______"></span><span id="___________FXDEVICE__ADDRESS_______"></span>**&lt; FxDevice 地址 &gt;**   
提供要显示的 FxDevice 的地址。

## <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 10 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

当 fxdevice 扩展出现在目标系统上时，它会显示以下信息。

-   非空闲 PoFx 设备
-   空闲 D0 PoFx 设备
-   空闲非 D0 PoFx 设备

下面的示例来自于！ fxdevice extension，其中包含提供的设备地址。

```dbgcmd
kd> !fxdevice ffffe0012ccbda60
!fxdevice 0xffffe0012ccbda60
    DevNode: 0xffffe0012bbb09f0
    UniqueId: "HDAUDIO\FUNC_01&VEN_10EC&DEV_0662&SUBSYS_103C304A&REV_1001\4&25ff998c&0&0001"
    InstancePath: "HDAUDIO\FUNC_01&VEN_10EC&DEV_0662&SUBSYS_103C304A&REV_1001\4&25ff998c&0&0001"
    Device Power State: PowerDeviceD0
    PEP Owner: Default PEP
    Acpi Plugin: 0
    Acpi Handle: 0
    Device Status Flags: IdleTimerOn DevicePowerNotRequired_ReceivedFromPEP 
    Device Idle Timeout: 0x1869ffffe7960
    Device Power On: No Activity
    Device Power Off: No Activity
    Device Unregister: No Activity
    Component Count: 1
        Component 0: F0/F0 - IDLE   (RefCount = 0)
        Pep Component: 0xffffe0012cfe1800
            Active: 0   Latency: 0  Residency: 0    Wake: 0 Dx IRP: 0   WW IRP: 0
            Component Idle State Change: No Activity
            Component Activation: No Activity
            Component Active: No Activity
```

下面是！ fxdevice 扩展中的默认输出。

```dbgcmd
kd> !fxdevice 
********************************************************************************
Dumping non-idle PoFx devices
********************************************************************************
!fxdevice 0xffffe0012bbd08d0
    DevNode: 0xffffe0012b3f87b0
    UniqueId: "\_SB.PCI0"
    InstancePath: "ACPI\PNP0A08\2&daba3ff&1"
    Device Power State: PowerDeviceD0
    Component Count: 1
        Component 0: F0/F1 - ACTIVE (RefCount = 28)

!fxdevice 0xffffe0012c587940
    DevNode: 0xffffe0012b3f9d30
    UniqueId: "\_SB.PCI0.PEGL"
    InstancePath: "PCI\VEN_8086&DEV_D138&SUBSYS_304A103C&REV_11\3&33fd14ca&0&18"
    Device Power State: PowerDeviceD0
    Component Count: 1
        Component 0: F0/F1 - ACTIVE (RefCount = 1)

...

********************************************************************************
Dumping idle D0 PoFx devices
********************************************************************************
!fxdevice 0xffffe0012c5838c0
    DevNode: 0xffffe0012bbdfd30
    UniqueId: "\_SB.PCI0.PCX1"
    InstancePath: "PCI\VEN_8086&DEV_3B42&SUBSYS_304A103C&REV_05\3&33fd14ca&0&E0"
    Device Power State: PowerDeviceD0
    Component Count: 1
        Component 0: F1/F1 - IDLE   (RefCount = 0)

!fxdevice 0xffffe0012c581ac0
    DevNode: 0xffffe0012bbdfa50
    UniqueId: "\_SB.PCI0.PCX5"
    InstancePath: "PCI\VEN_8086&DEV_3B4A&SUBSYS_304A103C&REV_05\3&33fd14ca&0&E4"
    Device Power State: PowerDeviceD0
    Component Count: 1
        Component 0: F1/F1 - IDLE   (RefCount = 0)

...
```

 

