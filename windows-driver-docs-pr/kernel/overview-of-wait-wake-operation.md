---
title: 等待/唤醒操作概述
description: 等待/唤醒操作概述
keywords:
- 电源管理 WDK 内核，唤醒功能
- 外部唤醒信号 WDK
- 唤醒设备
- 唤醒功能 WDK 电源管理
- 设备唤醒 ups WDK 电源管理
- IRP_MN_WAIT_WAKE
- 等待/唤醒 Irp WDK 电源管理，关于等待/唤醒 Irp
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 72d9012883e6913f6fea13abd0148e6549aa187b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808687"
---
# <a name="overview-of-waitwake-operation"></a>等待/唤醒操作概述





操作系统的唤醒机制的工作方式如下图所示。

![说明 irp \- mn \- 等待 \- 唤醒处理概述的示意图](images/send-waitwake.png)

1.  当系统和设备处于工作状态时，设备的电源策略所有者确定是否应启用其设备， ( 为唤醒 ) "已启用"。 电源策略所有者请求 power IRP ([**PoRequestPowerIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-porequestpowerirp) ，并使用次要代码 [**IRP \_ MN \_ WAIT \_ 唤醒**](./irp-mn-wait-wake.md)) 发送到其 PDO，以通知其设备堆栈中的所有驱动程序。 在请求中，策略所有者指定回调例程 (与 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程) 不同。

2.  通过 i/o 管理器将 IRP 发送到设备堆栈的顶部。

3.  驱动程序设置 *IoCompletion* 例程并将 IRP 向下传递，直到它到达总线驱动程序。

4.  总线驱动程序会在物理设备上启用唤醒功能（如果可以），并将 IRP 标记为挂起。 如果需要，它还会为其父代请求等待/唤醒 IRP。

5.  稍后，外部唤醒信号会到达。

6.  总线驱动程序完成 **IRP \_ MN \_ 等待 \_ 唤醒**。

7.  I/o 管理器会调用已设置为驱动程序的 *IoCompletion* 例程，并将 IRP 向下传递到堆栈中。

8.  当 i/o 管理器请求 IRP 时，它将调用策略所有者设置的回调例程。

**IRP \_ MN \_ WAIT \_ 唤醒** 请求不会更改设备或系统的电源状态。 它只是在设备上启用唤醒，以便以后在设备进入适当睡眠状态时，外部信号会导致设备 (，并且可能会) 系统唤醒。

唤醒信号到达时，无论设备是唤醒系统还是仅唤醒系统，驱动程序的行为都是相同的。 如果为设备启用了唤醒，并且系统处于休眠状态，则设备可以将其唤醒，设备会唤醒系统。 如果设备启用了唤醒，并且系统处于工作状态，则只有设备会唤醒。

由于计算机和设备的设计不同，特别是对于电源平面，因此，支持的系统和设备电源状态（以及可支持等待/唤醒的状态）在所有硬件配置上都不相同。 因此，任何拥有其设备电源策略的驱动程序和每个总线驱动程序都必须特别注意运行它的单个配置的功能。 有关详细信息，请参阅 [确定设备是否可以唤醒系统](determining-whether-a-device-can-wake-the-system.md)。

有关等待/唤醒操作的更多详细信息，请参阅 [通过设备树了解等待/唤醒 irp 的路径](understanding-the-path-of-wait-wake-irps-through-a-device-tree.md) 和 [等待/唤醒 Irp 完成的概述](overview-of-wait-wake-irp-completion.md)。

 

