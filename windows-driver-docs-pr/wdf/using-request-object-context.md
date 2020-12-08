---
title: 使用请求对象上下文
description: 使用请求对象上下文
keywords:
- 请求对象 WDK KMDF，上下文空间
- 上下文空间 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 031e380d4bef2c1648e375dca19089e173f7635b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827401"
---
# <a name="using-request-object-context"></a>使用请求对象上下文





每个框架请求对象（无论是由框架创建还是由驱动程序创建）都可以包含驱动程序定义的上下文空间。 当基于框架的驱动程序初始化框架设备对象时，驱动程序可以调用 [**WdfDeviceInitSetRequestAttributes**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetrequestattributes) 来指定 [**WDF \_ 对象 \_ 属性**](/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes) 结构，该结构描述设备的请求对象的上下文空间。

框架为请求对象分配上下文空间，如下所示：

-   当框架为驱动程序创建请求对象时，它会分配上下文空间，其中包含驱动程序在调用 **WdfDeviceInitSetRequestAttributes** 时指定的大小。

-   如果驱动程序通过调用 [**WdfRequestCreate**](/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcreate)来创建其他请求对象，则可以通过提供 WDF \_ 对象属性结构来指定上下文大小 \_ 。

有关为框架对象分配和访问上下文空间的详细信息，请参阅 [框架对象上下文空间](framework-object-context-space.md)。

 

