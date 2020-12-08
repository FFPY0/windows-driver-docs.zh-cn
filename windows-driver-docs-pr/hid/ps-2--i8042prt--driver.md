---
title: PS/2 (i8042prt) 驱动程序
description: 本主题介绍了 I8042prt 的功能，这是用于 PS/2 样式键盘和鼠标设备的 Microsoft Windows 2000 和更高版本的系统函数驱动程序。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b48f07d5544226ec9bec3bd2207b78d03b57af33
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820327"
---
# <a name="ps2-i8042prt-driver"></a>PS/2 (i8042prt) 驱动程序


本主题介绍了 *I8042prt* 的功能，这是用于 PS/2 样式键盘和鼠标设备的 Microsoft Windows 2000 和更高版本的系统函数驱动程序。

I8042prt 实现了 I8042prt 服务，并 i8042prt.sys 了其可执行映像。

I8042prt 的功能包括：

-   与硬件相关，同时操作 PS/2 样式键盘和鼠标设备。

    键盘和鼠标共享 i/o 端口，但使用不同的中断、中断服务例程 (ISR) 和 ISR 调度完成例程。

-   即插即用、电源管理和 WMI

-   旧设备的操作。

-   [键盘类服务回调例程](/windows-hardware/drivers/ddi/kbdmou/nc-kbdmou-pservice_callback_routine)和[鼠标类服务回调例程](/previous-versions/ff542363(v=vs.85))的连接。

    I8042prt 使用类服务回调将数据从 I8042prt 的输入数据缓冲区传输到类驱动程序的数据缓冲区。

-   添加了供应商提供的 [**PI8042 \_ 键盘设备的 \_ 初始化 \_ 例程**](/windows-hardware/drivers/ddi/ntdd8042/nc-ntdd8042-pi8042_keyboard_initialization_routine) 回调例程。

    可选的上层设备筛选器驱动程序提供回调例程。

-   添加供应商提供的 [**PI8042 \_ 键盘 \_ isr**](/windows-hardware/drivers/ddi/ntdd8042/nc-ntdd8042-pi8042_keyboard_isr) 回调例程和自定义 [**PI8042 \_ 鼠标 \_ isr**](/windows-hardware/drivers/ddi/ntdd8042/nc-ntdd8042-pi8042_mouse_isr) 回调例程。

    可选的高级设备筛选器驱动程序提供这些回调例程。

-   [键盘写入缓冲区请求](/windows-hardware/drivers/ddi/ntdd8042/ni-ntdd8042-ioctl_internal_i8042_keyboard_write_buffer) 和 [鼠标写入缓冲区请求](/windows-hardware/drivers/ddi/ntdd8042/ni-ntdd8042-ioctl_internal_i8042_mouse_write_buffer)。

    上层设备筛选器驱动程序可以使用写入缓冲区请求，将其写入操作与设备的 ISR 以及设备上的其他读取和写入操作同步到设备。

-   [键盘启动信息请求](/windows-hardware/drivers/ddi/ntdd8042/ni-ntdd8042-ioctl_internal_i8042_keyboard_start_information) 和 [鼠标启动信息请求](/windows-hardware/drivers/ddi/ntdd8042/ni-ntdd8042-ioctl_internal_i8042_mouse_start_information)。

    启动信息请求向顶级筛选器驱动程序传递指向设备中断对象的指针。 筛选器驱动程序可以使用中断对象将其操作与设备的 ISR 同步。

-   [I8042prt 回调例程](/windows-hardware/drivers/ddi/index)。

    上层设备筛选器驱动程序可以使用设备 ISR 的上下文中的回调例程来写入设备，并对来自设备的数据包进行排队。

### <a name="registry-settings-associated-with-the-ps2-driver"></a>与 PS/2 驱动程序关联的注册表设置

下面是与 PS/2 端口驱动程序相关联的注册表项的列表。

``` syntax
[Key: HKLM\SYSTEM\CurrentControlSet\Services\i8042prt\Parameters]
```

-   EnableWheelDetection \[ REG \_ DWORD \] –确定驱动程序是否试图检测并启用鼠标设备上的滚轮。 某些设备配备了鼠标轮来提供快速滚动和其他控制功能（如果应用程序支持）。
-   ResendIterations \[ REG \_ DWORD \] –指定尝试硬件操作的最大次数。 如果试验次数超过此项的值，Windows 将认为操作失败。
-   NumberOfButtons \[ REG \_ DWORD \] –指定启动时鼠标端口鼠标上的按钮数。 如果启动时检测到的按钮数量不正确，可以通过更改此项的值来覆盖它。
-   KeyboardDataQueueSize \[ REG \_ DWORD \] –指定键盘驱动程序缓冲区的键盘事件数。 此项还用于计算非分页内存池中键盘驱动程序的内部缓冲区的大小。 为了确定要为缓冲区分配的字节数，系统会将键盘输入数据结构的大小乘以 \_ \_ KeyboardDataQueueSize 的值。
-   PollStatusIterations \[ REG \_ DWORD \] –指定系统验证 i8042 控制器状态寄存器上的中断的最大次数。 如果无法在此项的值中指定的试验次数中验证中断，则会忽略中断。
-   PollingIterations \[ REG \_ DWORD \] -指定 Windows 2000 轮询硬件的最大次数。 如果超过了此项中指定的试验次数，Windows 2000 将停止轮询。
-   SampleRate \[ REG \_ DWORD \] –指定 ps/2 驱动程序测量 ps/2 鼠标的特征和活动的频率。 驱动程序使用通过采样收集的信息来优化鼠标设备的操作。
-   PollingIterationsMaximum \[ REG \_ DWORD \] –指定 Windows 2000 通过键盘上的旧版样式轮询硬件的最大次数。 如果超过了此项中指定的试验次数，则 Windows 将停止轮询。
-   MouseResendStallTime \[ REG \_ DWORD \] –确定如果在未确认的情况下返回重新发送消息，鼠标驱动程序将等待确认 (ACK) 。 当鼠标驱动程序中断服务例程包含 reset 时，将使用此项。
-   OverrideKeyboardType \[ REG \_ DWORD \] –指定键盘类型。 可以将此项添加到注册表中，以更正启动时检测到的键盘类型中的错误。
-   OverrideKeyboardSubtype \[ REG \_ DWORD \] –指定与 OEM 相关的键盘子类型。 可以将此项添加到注册表，以更正启动时检测到的键盘子类型中的错误。

有关详细信息，请参阅：

* [关于注册表](/windows/desktop/sysinfo/about-the-registry)
* [注册表引用](/windows/desktop/sysinfo/registry-reference)
