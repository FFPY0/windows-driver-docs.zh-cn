---
title: 适用于 WDF 驱动程序的 WDM 概念
description: 适用于 WDF 驱动程序的 WDM 概念
keywords:
- 内核模式驱动程序 WDK KMDF，WDM
- KMDF WDK，WDM
- Kernel-Mode Driver Framework WDK，WDM
- 基于框架的驱动程序 WDK KMDF，WDM
- WDM 驱动程序 WDK KMDF
- 总线枚举 WDK KMDF
- 总线驱动程序 WDK KMDF
- 函数驱动程序 WDK KMDF
- 筛选器驱动程序 WDK KMDF
- 驱动程序堆栈 WDK KMDF
- 堆栈 WDK KMDF
- 设备堆栈 WDK KMDF
- Irp WDK KMDF
- I/o 请求数据包 WDK KMDF
- I/o 请求 WDK KMDF，Irp
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c8235410e6c7867a6a7aea9c14a377487f845d2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840223"
---
# <a name="wdm-concepts-for-wdf-drivers"></a>适用于 WDF 驱动程序的 WDM 概念


Windows 驱动程序框架 (WDF) 是围绕 Microsoft Windows 驱动模型 (WDM) 接口的包装。 尽管该框架简化了许多 WDM 概念，并完全隐藏了其他概念，因此你不需要使用它们，但你仍应了解 WDM 驱动程序的一些基本概念。 具体而言，应了解 [驱动程序类型](#driver-types)、 [驱动程序堆栈](#driver-stacks)、 [设备堆栈](#device-stacks)和 [i/o 请求数据包](#io-request-packets)。

### <a name="driver-types"></a>驱动程序类型

基于 Windows 的驱动程序划分为三种类型： [总线驱动程序](../kernel/bus-drivers.md)、 [函数驱动程序](../kernel/function-drivers.md)和 [筛选器驱动](../kernel/filter-drivers.md)程序。 总线驱动程序通过检测插入到父总线并报告其特征的子设备，来支持 i/o 总线。  (此活动称为 " *总线枚举*"。 ) 函数驱动程序控制设备和总线的 i/o 操作。 筛选器驱动程序接收、查看并可能修改在用户应用程序和驱动程序之间或各个驱动程序之间流动的数据。

用于总线的驱动程序本质上是函数驱动程序，也会枚举子级。 驱动程序在枚举总线上的子设备时充当 "总线驱动程序"。 否则，在处理访问总线适配器硬件的 i/o 操作时，相同的驱动程序充当总线的 "函数驱动程序"。

User-Mode Driver Framework (UMDF) 驱动程序不能是总线驱动程序。

### <a name="driver-stacks"></a>驱动程序堆栈

在 Windows 操作系统中，WDM 驱动程序在称为 *驱动程序堆栈* 的垂直调用序列中分层。 堆栈中最顶层的驱动程序通常会在请求通过操作系统的 i/o 管理器后，从用户应用程序收到 i/o 请求。 通常，驱动程序层与计算机硬件通信。

简单的驱动程序堆栈在堆栈的底部包含一个总线驱动程序，该驱动程序处理特定于总线的 i/o 操作，并枚举连接到它的子设备。 通常，一个或多个特定于设备的函数驱动程序位于总线驱动程序之上。 这些函数驱动程序可处理连接到总线的设备的 i/o 操作。 筛选器驱动程序可以在函数驱动程序之上，也可以驻留在总线驱动程序和函数驱动程序之间。 正在运行的系统具有多个支持不同类型设备的驱动程序堆栈。

### <a name="device-stacks"></a>设备堆栈

每个驱动程序堆栈支持一个或多个 *设备堆栈*。 设备堆栈是从 WDM 定义的 [**设备 \_ 对象**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_device_object)结构创建的一组 *设备对象*。 每个设备堆栈代表一台设备。 每个驱动程序为其每个设备创建一个设备对象，并将每个设备对象附加到设备堆栈。 当设备插上并拔下并拔下设备堆栈，并且每次重新启动系统时，将会创建和删除设备堆栈。

当总线驱动程序检测到子设备已插入或拔下时，它会通知即插即用 (PnP) manager。 作为响应，PnP 管理器要求总线驱动程序为连接到父 (设备的每个子设备（即总线) ）创建物理设备对象 (PDO) 。 PDO 会成为设备堆栈的底部。

接下来，PnP 管理器加载函数和筛选器驱动程序以支持 (的每个设备) ，然后 PnP 管理器调用这些驱动程序，以便每个设备都可以创建设备对象并将其添加到设备堆栈的顶部。 函数驱动程序 (FDOs) 创建功能设备对象，筛选器驱动程序 (筛选器 DOs) 创建筛选器设备对象。

当 i/o 管理器将 i/o 请求发送到设备的驱动程序时，它会将该请求传递给在设备堆栈中创建最顶层设备对象的驱动程序。 如果该驱动程序要求 i/o 管理器将请求传递到下一个较低的驱动程序，则 i/o 管理器将使用设备堆栈确定下一个较低的驱动程序。  (下一个较低的驱动程序是创建下一个较低设备对象的驱动程序。 ) 

WDF 为每个 WDM 设备对象创建一个框架设备对象。 基于框架的驱动程序访问这些框架设备对象，而不是 WDM 设备对象。

### <a name="io-request-packets"></a>I/O 请求数据包

I/o 管理器通过 (Irp) 创建 i/o 请求数据包，将应用程序的 i/o 请求发送给驱动程序。 IRP 可以包含执行 i/o 操作的请求，如) 读取/写入操作，或请求执行 i/o 控制 (IOCTL) 操作 (例如返回状态)  (。 此外，PnP 管理器会创建代表驱动程序必须执行的 PnP 和电源管理操作的 Irp，并将这些 Irp 发送到驱动程序。

通常，当用户应用程序请求读取或写入操作时，i/o 管理器会创建一个读取或写入 IRP。 I/o 管理器将 IRP 传递到驱动程序堆栈顶部的驱动程序，该驱动程序将请求传递给下一个较低的驱动程序或向下传递请求。 某些请求会传递到堆栈的底部，一些请求将由较高级别的驱动程序完全处理。

每次驱动程序收到 IRP 时，驱动程序还会收到指向设备对象的指针，该对象表示必须处理操作的设备。 因此，驱动程序堆栈中的驱动程序使用设备对象来确定特定请求应使用的插入设备中的哪一个。

WDF 驱动程序通常不直接访问 Irp。 框架将表示读取、写入和设备 i/o 控制操作的 WDM Irp 转换为框架请求对象，这些对象 Kernel-Mode Driver Framework (KMDF) 和 UMDF 驱动程序在 i/o 队列中接收。 框架在内部处理 PnP 和电源管理 Irp，并使用事件回调函数通知驱动 PnP 和电源事件。

 

