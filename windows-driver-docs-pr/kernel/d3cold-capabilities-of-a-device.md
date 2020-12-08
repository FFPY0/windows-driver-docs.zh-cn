---
title: 设备的 D3cold 功能
description: 在作为电源策略所有者 (PPO) 的驱动程序启用设备后，设备可以输入 D3cold (当计算机停留在 S0) 时，驱动程序必须验证设备是否响应并在设备进入 D3cold 后继续正常运行。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: cd84b86ee7bd2d9c006064aff69c49bc70711a15
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792811"
---
# <a name="d3cold-capabilities-of-a-device"></a>设备的 D3cold 功能


在作为电源策略所有者 (PPO) 的驱动程序启用设备后，设备可以输入 D3cold (当计算机停留在 S0) 时，驱动程序必须验证设备是否响应并在设备进入 D3cold 后继续正常运行。

对于即插即用 (PnP) 设备，操作系统通常从父总线驱动程序获取有关设备的 D3cold 功能的信息。

例如，如果将设备连接到 PCI Express 或 PCI Express 总线，则设备的 PCI 配置空间将包含表示设备功能的电源管理注册块。 此块中的功能标志指定设备的电源状态，设备可以使用该电源状态向唤醒事件) 的 PCI 术语发出电源管理事件或 PME (。 这些状态可能包括 D3hot 和 D3cold。 有关 PCI 电源管理的详细信息，请参阅 [Pci 总线电源管理接口规范](https://pcisig.com/specifications/conventional/pci_bus_power_management_interface/)。

如果设备必须能够从其输入的任何低功耗 Dx 状态向唤醒事件发出信号，则设备不应输入 D3cold，除非设备、父总线控制器和硬件平台支持从 D3cold 发出唤醒事件。

设备的 KMDF 驱动程序将调用 [**WdfDeviceAssignS0IdleSettings**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceassigns0idlesettings) 方法，以使设备能够在设备可用于传输唤醒事件的最小设备电源状态中处于空闲状态。 从 KMDF 版本1.11 开始， **WdfDeviceAssignS0IdleSettings** 在可能的低功耗 Dx 状态范围内包含 D3cold。 仅当设备、父总线驱动程序和 ACPI 系统固件支持 D3cold 发出的唤醒事件时，此方法才允许设备在 D3cold 中空闲。

设备的 WDM 驱动程序必须决定设备处于空闲状态时要将设备移动到哪种低功耗 Dx 状态。  (相反， **WdfDeviceAssignS0IdleSettings** 会自动选择此 Dx 状态，以便驱动程序无需。 ) 如果设备必须能够从其输入的任何低功耗 Dx 状态发出唤醒事件信号，则驱动程序可以调用 [*GetIdleWakeInfo*](/windows-hardware/drivers/ddi/wdm/nc-wdm-get_idle_wake_info) 例程来确定设备可用于向唤醒事件发出信号的设备电源状态。 为获取此信息， *GetIdleWakeInfo* 会查询底层总线驱动程序和 ACPI 系统固件。 根据 *GetIdleWakeInfo* 中的信息，驱动程序可以调用 [*SetD3ColdSupport*](/windows-hardware/drivers/ddi/wdm/nc-wdm-set_d3cold_support) 例程来启用或禁用设备到 D3cold 的转换。

设备可能不需要能够从 D3cold 发出唤醒事件。 仅当响应软件启动的操作时，才可以将设备设置为仅允许从 D3cold 到 D0 的转换。 例如，如果驱动程序收到设备的 i/o 请求，驱动程序可能需要唤醒设备。 除了少数例外情况，此类设备的驱动程序可以使设备进入 D3cold。 一个可能的例外是需要很长时间才能将 D3cold 转换为 D0 的设备。 例如，显示设备可能包含大量需要在设备进入 D3cold 之前保存并在设备退出 D3cold 之后进行还原的内存。

有关 D3cold 的 ACPI 支持的详细信息，请参阅 [D3cold 的固件要求](../bringup/firmware-requirements-for-d3cold.md)。

 

