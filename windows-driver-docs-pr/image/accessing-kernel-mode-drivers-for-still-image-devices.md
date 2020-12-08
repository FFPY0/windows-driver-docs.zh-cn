---
title: 访问适用于静态图像设备的内核模式驱动程序
description: 访问适用于静态图像设备的内核模式驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67e0a12f3de92f80ed4a1fca51d7ace365e1e1ce
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808305"
---
# <a name="accessing-kernel-mode-drivers-for-still-image-devices"></a>访问适用于静态图像设备的内核模式驱动程序





Microsoft 提供基于 WDM 的内核模式驱动程序，以支持连接到 SCSI 和 USB 总线的静止图像设备。 这两个驱动程序都支持即插即用设备，并提供服务，用于添加、删除、启动、停止和创建即插即用设备的注册表项。 此外，这两个驱动程序都提供对支持电源管理的设备的挂起和恢复操作。

用户模式静止图像微型驱动程序可以通过调用 Microsoft Windows SDK 文档) 中所述的 [**CreateFile**](/windows/win32/api/fileapi/nf-fileapi-createfilea)、 **ReadFile**、 **WriteFile** 和 [**DeviceIoControl**](/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol) (来访问这些内核模式驱动程序。 **ReadFile** 和 **WriteFile** 用于块数据传输。 具体而言，将调用 **ReadFile** 来获取图像数据，并使用 **WriteFile** 将命令发送到接受作为数据流的命令的设备。

在调用 **ReadFile**、 **Writefile** 或 [**DeviceIoControl**](/windows/win32/api/ioapiset/nf-ioapiset-deviceiocontrol)之前，微型驱动程序必须调用 [**IStiDeviceControl：： GetMyDevicePortName**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istidevicecontrol-getmydeviceportname) 以获取设备的端口名称，然后将该端口名称用作 [**CreateFile**](/windows/win32/api/fileapi/nf-fileapi-createfilea)的参数。

[SCSI 驱动程序](scsi-driver.md)

[USB 驱动程序](usb-driver.md)

 

