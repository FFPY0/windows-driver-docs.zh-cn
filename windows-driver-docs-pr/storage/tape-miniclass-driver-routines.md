---
title: 磁带微型类驱动程序例程
description: 磁带微型类驱动程序例程
keywords:
- 磁带驱动程序 WDK 存储，可选例程
- 存储磁带驱动程序 WDK，可选例程
- 磁带驱动程序 WDK 存储，必需例程
- 存储磁带驱动程序 WDK，必需例程
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: c3e7405c9f9ad8c92b06bf656c85b439b2bf7c07
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820483"
---
# <a name="tape-miniclass-driver-routines"></a>磁带微型类驱动程序例程

磁带 miniclass 驱动程序必须具有以下例程：

- [**DriverEntry**](driverentry-of-tape-miniclass-driver.md) 提供了由磁带类驱动程序用来初始化 miniclass 驱动程序的特定于驱动程序的入口点和常量。

  磁带 miniclass 驱动程序的 **DriverEntry** 例程分配 TAPE_INIT_DATA_EX 结构，在结构中设置特定于驱动程序的常量和入口点，并在磁带机中调用 **TapeClassInitialize** 。

- 为设备控制请求实现特定于设备的处理的例程，如 TapeMiniGetPosition 和 TapeMiniGetMediaTypes。

  磁带类驱动程序从其设备控制调度例程调用这样的例程。 有关详细信息，请参阅 [处理磁带设备控制请求](processing-tape-device-control-requests.md)。

磁带 miniclass 驱动程序可以具有以下可选例程：

- *TapeMiniExtensionInit* 初始化可选的 minitape 扩展。

  有关 minitape 扩展的信息，请参阅 [在可选扩展中存储磁带 Miniclass 上下文](storing-tape-miniclass-context-in-optional-extensions.md) 。

- *TapeMiniTapeError* 对磁带类驱动程序的错误处理进行了补充。

  对于大多数设备，当发生错误时，如果不从磁带 miniclass 驱动程序输入，则磁带类驱动程序可以返回相应的状态值。 但对于某些设备，磁带类驱动程序需要来自磁带 miniclass 驱动程序的设备特定信息以返回相应的状态。 例如，4mm DAT 磁带驱动器的 miniclass 驱动程序可以确定，在某些情况下，TAPE_STATUS_BUS_RESET 状态实际上是因为驱动器中没有介质。 4mm DAT miniclass driver 的 *TapeMiniTapeError* 例程将识别这些情况，并将返回的状态更改 TAPE_ERROR_NO_MEDIA。

磁带 miniclass 驱动程序的 **DriverEntry** 例程必须严格使用该名称，才能由操作系统自动加载。 只要例程的入口点在 TAPE_INIT_DATA_EX 结构中设置，就可以选择将 *TapeMiniXxx* 例程命名为驱动程序编写器。 为了帮助进行调试，miniclass 驱动程序应在 *TapeMiniXxx* 例程前面加上一些字符来标识自身，并确保名称中的其余字符反映例程的作用。

磁带 miniclass 驱动程序所需的例程、结构和常量是在 *minitape* 中声明的。

有关磁带类例程的信息，请参阅 [磁带类驱动程序例程](tape-class-driver-routines.md)。
