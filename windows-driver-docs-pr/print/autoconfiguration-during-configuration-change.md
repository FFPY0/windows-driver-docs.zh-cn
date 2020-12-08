---
title: 配置更改期间的自动配置
description: 配置更改期间的自动配置
keywords:
- 配置更改期间自动配置 WDK 打印机
- 在配置更改期间打印机自动配置 WDK 打印机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 032e587777e1812fcca61ce1fbc0233fc0a2e571
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836093"
---
# <a name="autoconfiguration-during-configuration-change"></a>配置更改期间的自动配置


安装设备后，端口监视器负责通过发送事件或通过轮询使配置数据保持最新。 只要驱动程序或应用程序对设备的当前配置感兴趣，就可以使用 [双向通信接口](/windows-hardware/drivers/ddi/_print/index) 和 [双向通信架构](./bidi-communications-schema-reference.md) 来查询端口监视器以获取此信息。

下图显示了设备的配置更改时在自动配置中的数据流：

![说明设备配置更改时在自动配置过程中的数据流的关系图](images/autocfgcfgchange.png)

1.  当设备配置发生更改时，使用 Web 服务事件 (WS 事件) 协议的设备会通知打印子系统其状态已更改，但不描述特定的更改。 标准 TCP/IP 端口监视器对不支持 WS 事件的设备进行轮询。

2.  端口监视器生成设备配置已更改的通知，并将通知发送到后台处理程序。

3.  后台处理程序通过 `DrvPrinterEvent` 在调用中调用并传递打印机 \_ 事件 \_ 配置更新来向驱动程序发送通知 \_ 。 此函数调用用于通知驱动程序设备的配置已更改。

驱动程序可以确定设备的配置何时发生更改，因为通知消息会包含更改的值， (在双向通知设计规范) 中定义架构。 但是，如果通知太大而无法通过通知机制发送，则通知将有一个或多个 ReducedSchema 实例，其中每个实例都表示设备特征已更改，但没有其新值的任何详细信息。

 

