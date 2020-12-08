---
title: 可选和必需的 GPIO 回调函数
description: 常规用途 i/o (GPIO) 控制器驱动程序调用 GPIO_CLX_RegisterClient 方法，以注册为 GPIO framework 扩展的客户端 (GpioClx) 。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0588e5944dd355a38f1c88917b7056db29915d5a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827213"
---
# <a name="optional-and-required-gpio-callback-functions"></a>可选和必需的 GPIO 回调函数


常规用途 i/o (GPIO) 控制器驱动程序调用 [**gpio \_ CLX \_ RegisterClient**](/windows-hardware/drivers/ddi/gpioclx/nf-gpioclx-gpio_clx_registerclient) 方法，以注册为 Gpio framework 扩展 (GpioClx) 的客户端。 在此调用期间，驱动程序将注册数据包传递到 GpioClx，后者指定由驱动程序实现的事件回调函数的列表。 GpioClx 调用这些回调函数来配置 GPIO 控制器硬件、执行 i/o 操作和管理中断。 GpioClx 要求使用 GPIO 控制器驱动程序来实现某些回调函数，但对其他回调函数的支持是可选的。

注册数据包是 [**GPIO \_ 客户端 \_ 注册 \_ 数据包**](/windows-hardware/drivers/ddi/gpioclx/ns-gpioclx-_gpio_client_registration_packet) 的结构。 如果 GPIO 控制器驱动程序实现特定的回调函数，它会将该回调函数的函数指针写入此结构的相应成员。 或者，若要指示特定的回调函数不受支持，驱动程序会将 NULL 写入相应的成员。

注册数据包中必须包含以下回调函数：

[*客户端 \_PrepareController*](/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_prepare_controller) 
 [*client \_ QueryControllerBasicInformation*](/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_query_controller_basic_information) 
 [*client \_ StartController*](/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_start_controller) 
 [*client \_ StopController*](/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_stop_controller) 
 [*client \_ ReleaseController*](/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_release_controller)如果缺少前面列表中的任何回调函数 (也就是说，如果注册包中的相应函数指针为 NULL) ， **GPIO \_ CLX \_ RegisterClient** 方法将失败。

不需要使用 GPIO 控制器驱动程序来支持读取或写入 GPIO i/o 引脚，这是配置为数据输入或数据输出的 pin。  (没有 i/o pin 的 GPIO 控制器仍可以从外围设备中继中断请求 ) 。但是，如果注册数据包包含以下与 i/o 相关的回调函数之一，则数据包必须包含以下两个回调函数：

[*客户端 \_ConnectIoPins*](/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_connect_io_pins) 
 [*CLIENT \_ DisconnectIoPins*](/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_disconnect_io_pins)另外，如果注册数据包包含上述列表中的两个回调函数，则驱动程序还必须支持从 gpio i/o 引脚读取、写入 gpio i/o pin 或同时支持这两者。 具体而言，注册数据包必须至少包含以下列表中的一个回调函数：

[*客户端 \_ReadGpioPins*](/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_read_pins)或 [*client \_ ReadGpioPinsUsingMask*](/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_read_pins_mask) 
 [*client \_ WriteGpioPins*](/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_write_pins)或 [*client \_ WriteGpioPinsUsingMask*](/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_write_pins_mask)支持读取的驱动程序必须实现前面列表中的两个 *客户端 \_ ReadGpioPins* Xxx 回调函数之一。 支持写入的驱动程序必须实现前面列表中的两个 *客户端 \_ WriteGpioPins* Xxx 回调函数之一。

实现 *客户端 \_ ReadGpioPinsUsingMask* 和/或 *客户端 \_ WriteGpioPinsUsingMask* 的驱动程序必须在 [*客户端 \_ QueryControllerBasicInformation*](/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_query_controller_basic_information)回调函数提供的设备信息中设置 **FormatIoRequestsAsMasks** 标志位。 实现 *客户端 \_ ReadGpioPins* 和/或 *客户端 \_ WriteGpioPins* 的驱动程序不得设置此标志位。 有关详细信息，请参阅 [**客户端 \_ 控制器 \_ 基本 \_ 信息**](/windows-hardware/drivers/ddi/gpioclx/ns-gpioclx-_client_controller_basic_information)中 **标志** 成员的说明。

无需使用 GPIO 控制器驱动程序来支持 GPIO 中断。 但是，如果注册数据包包含以下任何中断相关的回调函数，则数据包必须包含以下所有回调函数：

[*客户端 \_EnableInterrupt*](/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_enable_interrupt) 
 [*client \_ DisableInterrupt*](/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_disable_interrupt) 
 [*client \_ MaskInterrupts*](/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_mask_interrupts) 
 [*client \_ QueryActiveInterrupts*](/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_query_active_interrupts) 
 [*client \_ UnmaskInterrupt*](/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_unmask_interrupt)支持中断屏蔽的驱动程序必须实现 *客户端 \_ MaskInterrupts* 回调函数。 支持查询活动中断的驱动程序必须实现 *客户端 \_ QueryActiveInterrupts* 回调函数。

[*客户端 \_ ClearActiveInterrupts*](/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_clear_active_interrupts)回调函数是一种特殊情况。 如果在读取时 GPIO 控制器硬件自动清除活动中断，则不需要 *客户端 \_ ClearActiveInterrupts* 函数，并且应将注册数据包中的相应函数指针设置为 NULL。 但是，如果在读取活动中断时未自动清除活动中断，并且注册数据包中提供了前面列表中与中断相关的回调函数，则必须将 *客户端 \_ ClearActiveInterrupts* 函数包含在包中。 若要指示在读取时硬件自动清除活动中断，驱动程序会在 [*客户端 \_ QueryControllerBasicInformation*](/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_query_controller_basic_information)回调函数提供的设备信息中设置 **ActiveInterruptsAutoClearOnRead** 标志位。 有关详细信息，请参阅 [**客户端 \_ 控制器 \_ 基本 \_ 信息**](/windows-hardware/drivers/ddi/gpioclx/ns-gpioclx-_client_controller_basic_information)中 **标志** 成员的说明。

如果 GPIO 控制器驱动程序支持 GPIO 中断，则注册数据包可作为选项，包括以下回调函数：

[*客户端 \_QueryEnabledInterrupts*](/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_query_enabled_interrupts) GpioClx 支持从 Windows 8.1 开始的 *客户端 \_ QueryEnabledInterrupts* 函数。

支持 [组件级电源管理](../kernel/component-level-power-management.md) 的驱动程序必须实现以下两个回调函数：

[*客户端 \_RestoreBankHardwareContext*](/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_restore_bank_hardware_context) 
 [*client \_ SaveBankHardwareContext*](/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_save_bank_hardware_context)若要指示硬件支持组件级电源管理，驱动程序会在 [*客户端 \_ QueryControllerBasicInformation*](/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_query_controller_basic_information)回调函数提供的设备信息中设置 **BankIdlePowerMgmtSupported** 标志位。 有关详细信息，请参阅 [**客户端 \_ 控制器 \_ 基本 \_ 信息**](/windows-hardware/drivers/ddi/gpioclx/ns-gpioclx-_client_controller_basic_information)中 **标志** 成员的说明。

[*客户端 \_ PreProcessControllerInterrupt*](/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_pre_process_controller_interrupt)、[*客户端 \_ ReconfigureInterrupt*](/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_reconfigure_interrupt)和 [*客户端 \_ ControllerSpecificFunction*](/windows-hardware/drivers/ddi/gpioclx/nc-gpioclx-gpio_client_controller_specific_function)回调函数是可选的，由 GpioClx 支持，以解决某些 GPIO 控制器实现中特定于硬件的问题。 只有具有特殊要求的 GPIO 控制器驱动程序才能实现这些功能。

 

