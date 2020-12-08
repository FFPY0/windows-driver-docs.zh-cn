---
title: 创建 SAN 的服务提供程序
description: 创建 SAN 的服务提供程序
keywords:
- Windows 套接字直接 WDK，服务提供商
- SAN 服务提供商 WDK，创建
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e6a51d7626f60ed8c251b8c9c884120867565823
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823037"
---
# <a name="creating-a-service-provider-for-a-san"></a>创建 SAN 的服务提供程序





本部分简要说明了构成 SAN 服务提供程序 DLL 和 Windows 套接字交换机之间的接口的功能。 SAN 服务提供程序 DLL 为其初始化函数 [**WSPStartupEx**](/previous-versions/windows/hardware/network/ff566321(v=vs.85))导出单个入口点。 SAN 服务提供商的 **WSPStartupEx** 功能反过来使 Windows 套接字交换机可以通过调度表访问大多数其他接口功能。 剩余的接口函数通过对 SAN 服务提供程序的 [**WSPIoctl**](/previous-versions/windows/hardware/network/ff566296(v=vs.85)) 函数的调用提供给开关。 接口函数包括 [Windows 套接字 spi 函数](windows-sockets-spi-functions-required-for-sans.md) 和 [WINDOWS 套接字 spi 接口的特定于 SAN 的扩展](windows-sockets-spi-extensions-for-sans.md)。

[Windows Socket 直接参考](/previous-versions/windows/hardware/network/ff565857(v=vs.85))提供了有关在 SAN 服务提供程序中实现的这些功能的详细信息。 请勿使用 Windows 套接 SPI 函数的 Microsoft Windows SDK 说明。 Windows SDK 说明不包含特定于 SAN 的要求。

本部分还列出了 [不需要 SAN 服务提供商提供的 Windows 套接 SPI 函数](windows-sockets-spi-functions-not-required-for-sans.md)。

 

