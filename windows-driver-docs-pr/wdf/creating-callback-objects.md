---
title: 创建回调对象
description: 创建回调对象
keywords:
- 回叫对象 WDK UMDF
- 回叫对象 WDK UMDF，创建
- User-Mode Driver Framework WDK，对象
- 用户模式驱动程序 WDK UMDF，对象
- UMDF 对象 WDK，回调对象
- framework 对象 WDK UMDF，回调对象
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 438d6046ff3a9ef9c83e6515baacd3766c5c5d7e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829029"
---
# <a name="creating-callback-objects"></a>创建回调对象


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

UMDF 驱动程序可以创建 *回调对象*，后者包含上下文数据和接口方法。 框架通过驱动程序的回调接口方法访问驱动程序的回调对象。

下图显示了驱动程序实现的回调对象如何与 [框架对象](framework-objects.md)相对应。

![框架对象和供应商提供的回调对象](images/correspond.gif)

UMDF 驱动程序可以创建几种类型的回调对象，其中包括：

-   驱动程序回调对象

    框架使用驱动程序回调对象初始化驱动程序，并通知驱动程序已到达新设备。

-   设备回调对象

    驱动程序使用设备回调对象来存储设备上下文，并处理清理和关闭文件对象，并即插即用 (PnP) 和电源管理 (PM) 事件。

-   队列回调对象

    驱动程序使用队列回调对象来处理 i/o。

下图显示了 UMDF 驱动程序如何创建设备回调对象。

![用于创建 umdf 设备回调对象的调用序列](images/callback.gif)

以下主题包含演示如何创建回调对象的代码示例：

-   [创建回调对象示例](creating-callback-objects-example.md)

-   [定义回调对象示例](defining-callback-objects-example.md)

-   [关联回调接口示例](associating-callback-interfaces-example.md)

 

 





