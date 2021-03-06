---
description: WPD 驱动程序示例
title: WPD 驱动程序示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 88ae7070cc419914a756a141287f93e742ea36a2
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91734341"
---
# <a name="the-wpd-driver-samples"></a>WPD 驱动程序示例


Windows 便携设备驱动程序工具包包含五个示例 WPD 驱动程序。 下表对这些驱动程序进行了简要说明。 有关这些驱动程序的更详细说明，请参阅文档。

**注意**   如果你不熟悉 WPD 驱动程序模型，请从 WpdHelloWorldDriver 开始。

 

| 示例                                                            | 说明                                                                                                                                                                                    |
|-------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [WpdHelloWorldDriver](the-sample-driver-architecture.md)         | 支持单个设备对象和多个只读属性的基本示例驱动程序。 此驱动程序模拟硬件交互。                                                      |
| [WpdBasicHardwareDriver](the-wpdbasichardwaredriver-sample.md)   | 与简单传感器交互的示例驱动程序。 此驱动程序允许 WPD 应用程序接收传感器数据，并设置数据到达的时间间隔。                             |
| [WpdMultiTransportDriver](the-wpdmultitransportdriver-sample.md) | 一个示例驱动程序，演示如何为支持多个传输的设备创建单个访问点。 此驱动程序模拟硬件交互。                              |
| [WpdWudfSampleDriver](the-wpdwudfsampledriver-sample.md)         | 一个全面的示例驱动程序，演示 WPD 设备驱动程序接口 (DDI) 。 此示例驱动程序模拟硬件交互。                                                      |
| [WpdServiceSampleDriver](the-wpdservicesampledriver-sample.md)   | 演示支持联系人服务的示例驱动程序。  (服务是 WPD 支持的功能对象的扩展。 ) 此驱动程序模拟硬件交互。 |

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[WPD HelloWorld 驱动程序下载页](/samples/browse/)

[WPD 基本硬件驱动程序下载页](/samples/browse/)

[WPD 多传输驱动程序下载页](/samples/browse/)

[WPD 服务示例驱动程序下载页](/samples/browse/)

[WPD WUDF 示例驱动程序下载页](/samples/browse/)

 

