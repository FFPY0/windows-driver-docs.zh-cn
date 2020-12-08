---
title: UMDF 的体系结构
description: 本主题介绍了驱动程序管理器如何生成用户模式设备堆栈，以及主机进程、反射器和驱动程序管理器如何处理应用程序发送到 User-Mode Driver Framework (UMDF) 驱动程序的 i/o 请求。
keywords:
- User-Mode Driver Framework WDK、体系结构
- UMDF WDK，体系结构
- 用户模式驱动程序 WDK UMDF、体系结构
- 体系结构 WDK UMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98e92b2fc831842ff6713e97ec4a6e29220c2884
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837031"
---
# <a name="architecture-of-umdf"></a>UMDF 的体系结构


本主题介绍了驱动程序管理器如何生成用户模式设备堆栈，以及主机进程、反射器和驱动程序管理器如何处理应用程序发送到 User-Mode Driver Framework (UMDF) 驱动程序的 i/o 请求。

类似于内核模式堆栈，用户模式堆栈的构造和细分由即插即用 (PnP) 事件驱动。 构建内核模式堆栈后，反射器会通知驱动程序管理器开始构造用户模式堆栈。 驱动程序管理器将启动驱动程序主机进程，并为启动的进程提供足够的信息以生成用户模式堆栈。 通过这种方式，可以将用户模式堆栈视为内核模式堆栈的扩展。

驱动程序主机进程为用户模式驱动程序提供执行环境，并在用户模式堆栈中的驱动程序之间路由消息。 反射器使用基于消息的进程间通信机制来与驱动程序管理器和主机进程通信。

![umdf 组件在反射器中包含向上和向下设备对象](images/umdfarch4.gif)

若要将 i/o 请求发送到 UMDF 驱动程序，应用程序需要调用 Win32 文件 i/o 函数，例如 [**CreateFile**](/windows/win32/api/fileapi/nf-fileapi-createfilea)、 **ReadFileEx**、 **CancelIoEx** 或 [**DeviceIoControl**](/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol)。 当反射器接收来自客户端应用程序的请求时，它会将请求发送到相应的驱动程序主机进程。 然后，驱动程序主机进程将请求路由到正确的用户模式设备堆栈的顶部。

请求已由用户模式堆栈中的某个驱动程序完成，或由驱动程序的一个驱动程序转发回反射器。 当反射器接收到来自用户模式驱动程序堆栈的请求时，它会向下发送请求的内核模式堆栈。

 

