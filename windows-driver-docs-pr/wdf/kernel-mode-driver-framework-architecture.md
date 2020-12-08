---
title: WDF 体系结构
description: WDF 体系结构
keywords:
- 内核模式驱动程序 WDK KMDF、体系结构
- KMDF WDK，体系结构
- Kernel-Mode Driver Framework WDK、体系结构
- 对象方法 WDK KMDF
- 体系结构 WDK KMDF
- 对象事件回调函数 WDK KMDF
- 事件回调函数 WDK KMDF
- 对象属性 WDK KMDF
- 对象处理 WDK KMDF
- 接口 WDK KMDF
- 对象 WDK KMDF
- framework 对象 WDK KMDF，体系结构
- 基于框架的驱动程序 WDK KMDF，体系结构
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b552acea66923bac23de7aa7a830a505b45fd98d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796363"
---
# <a name="wdf-architecture"></a>WDF 体系结构





WDF 为驱动程序提供了基于对象的接口。 框架定义的对象接口包含：

<a href="" id="object-methods"></a>*对象方法*  
方法是驱动程序可以调用以对对象执行操作或获取或设置对象属性的函数。 方法名为 **Wdf**_ObjectAction_，其中 *对象* 描述对象， *操作* 指示函数的作用。 例如， [**WdfDeviceCreate**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate) 创建设备对象。

<a href="" id="object-event-callback-functions"></a>*对象事件回调函数*  
事件回调函数是驱动程序提供的函数。 每个事件回调函数都与某个对象上可能发生的特定事件相关联。 当发生关联的事件时，框架将调用事件回调函数。 按照约定，事件回调函数的占位符称为 .Evt *register-objectevent*，不过，你可以将这些回调命名为驱动程序中所选的任何内容。 例如，驱动程序将注册 [*EvtDeviceD0Entry*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_d0_entry) 事件回调，以便在设备进入工作状态时收到通知。

<a href="" id="object-properties"></a>*对象属性*  
属性是存储在对象中的值，并且驱动程序可以 *获取* (即，获取) 并 *设置* (，即更改) 。 在许多情况下，属性将直接映射到相应 WDM 对象中的字段。 不能失败的属性命名为 **wdf**_对象_*_获取_*_值_ 和 **Wdf**_对象_*_集_*_值_，并且可能失败的属性被命名为 **wdf**_对象_*_检索_*_值_ 和 **wdf**_对象_*_赋值_*_。_ *对象* 描述对象， *值* 标识函数设置或返回的数据。 例如， [**WdfDeviceGetDriver**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicegetdriver) 返回与设备对象相关联的驱动程序对象的句柄。

<a href="" id="object-handles"></a>*对象句柄*  
基于框架的驱动程序绝不会直接访问框架对象。 相反，驱动程序将接收对象句柄，该句柄可传递给对象的方法。

框架定义了基于框架的驱动程序使用的多种对象类型：

-   *框架驱动程序对象* 表示每个驱动程序。

-   *框架设备对象* 表示驱动程序支持的每个设备。

-   *框架队列对象* 代表接收设备 i/o 请求的 i/o 队列。

-   *Framework 请求对象* 表示每个 i/o 队列接收的 i/o 请求数。

有关框架定义的所有对象的列表，请参阅 [框架对象的摘要](summary-of-framework-objects.md)。

 

