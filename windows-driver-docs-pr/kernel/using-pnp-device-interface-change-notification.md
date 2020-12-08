---
title: 使用 PnP 设备接口更改通知
description: 使用 PnP 设备接口更改通知
keywords:
- 通知 WDK PnP，设备接口更改
- EventCategoryDeviceInterfaceChange 通知
- 设备接口更改通知 WDK PnP
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: d135d3cf5b9f3493e6c111292a67954ddd1d174b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816043"
---
# <a name="using-pnp-device-interface-change-notification"></a>使用 PnP 设备接口更改通知





驱动程序注册 **EventCategoryDeviceInterfaceChange** 通知，以便在 (启用特定类的设备接口时通知驱动程序) 或删除计算机 (禁用) 。 例如，复合电池驱动程序可能会注册类电池的设备接口通知，因此它可以向操作系统提供有关可用电池电量总计的信息。

以下小节讨论了如何注册设备接口更改通知，以及如何在 PnP 通知回调例程中处理设备接口更改事件：

[注册设备接口更改通知](registering-for-device-interface-change-notification.md)

[处理设备接口更改事件](handling-device-interface-change-events.md)

有关设备接口的信息，请参阅 [**IoRegisterDeviceInterface**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface) 和相关例程。

 

