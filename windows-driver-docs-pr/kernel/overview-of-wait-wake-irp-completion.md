---
title: 等待/唤醒 IRP 完成概述
description: 等待/唤醒 IRP 完成概述
keywords:
- 电源管理 WDK 内核，唤醒功能
- 外部唤醒信号 WDK
- 唤醒设备
- 唤醒功能 WDK 电源管理
- 设备唤醒 ups WDK 电源管理
- IRP_MN_WAIT_WAKE
- 等待/唤醒 Irp WDK 电源管理，完成
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85ebde47e108c5280a4275e14bc938d846f87fbc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831355"
---
# <a name="overview-of-waitwake-irp-completion"></a>等待/唤醒 IRP 完成概述





等待/唤醒 IRP 在唤醒信号到达时完成。 唤醒信号特定于设备，但通常是设备的正常服务事件。 例如，传入环可能会导致休眠的调制解调器唤醒。

下图显示了完成等待/唤醒 IRP 的步骤。

![完成等待/唤醒 irp 的步骤](images/comp-waitwake.png)

当信号发生时，控制将在总线检测到设备已唤醒的点重新进入总线驱动程序。 总线驱动程序会根据需要向事件提供服务，并调用 [**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) 来完成 [**IRP \_ MN \_ 等待 \_ 唤醒**](./irp-mn-wait-wake.md) IRP 的 PDO。

然后，i/o 管理器会调用设备堆栈中下一个更高的驱动程序设置的 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程。 在 *IoCompletion* 例程中，该驱动程序将根据需要为唤醒信号服务，并调用 **IOCOMPLETEREQUEST** 来完成 IRP。 在所有驱动程序都完成 IRP 之前，i/o 管理器会继续调用在设备堆栈上工作的 *IoCompletion* 例程。

在其 *IoCompletion* 例程中，任何枚举多个子设备 (的驱动程序会创建多个 PDO) 并收到来自多个此类设备的等待/唤醒请求。必须向其自身发送等待/唤醒 IRP，使其自行重入等待/唤醒。 有关详细信息，请参阅 [通过设备树了解等待/唤醒 irp 的路径](understanding-the-path-of-wait-wake-irps-through-a-device-tree.md)。

在调用由驱动程序设置的 *IoCompletion* 例程后，当它们向下传递 IRP 时，i/o 管理器会调用电源策略所有者在请求 wait/唤醒 IRP 时设置的回调例程。 在回调例程中，策略所有者应将其设备返回到工作状态，并为其子 PDO 完成挂起的等待/唤醒 IRP （如果有）。

完成子项的 IRP 会导致 i/o 管理器调用由子设备堆栈中的驱动程序设置的 *IoCompletion* 例程，依此类推。 最终，在 devnode 上启动原始等待/唤醒 IRP 的策略所有者决定其设备已断言唤醒信号，并且所有挂起的等待/唤醒 Irp 都将完成。

 

