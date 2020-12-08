---
title: 关于存储驱动程序和设备对象
description: 存储驱动程序和设备对象
keywords:
- 存储驱动程序 WDK，设备对象
- 设备对象 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69e1169bd0315d0753e6dbf308eaffa3d0c2b423
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799313"
---
# <a name="about-storage-drivers-and-device-objects"></a>关于存储驱动程序和设备对象

存储设备堆栈包含由驱动程序创建的设备对象树，这些驱动程序由处理系统上存储设备的 i/o 所涉及。 此树的根是 (FDO) 用于存储适配器或与存储堆栈集成的其他驱动程序堆栈的功能设备对象。 此树的叶是设备对象，供文件系统和用户模式应用程序使用。

与任何 PnP 驱动程序一样，存储类或存储筛选器驱动程序通过使用 **IoCreateDevice** 创建设备对象，并使用 **IoAttachDeviceToDeviceStack** 将其附加到设备堆栈中，将其自身添加到树中的 AddDevice 例程，并使用指针连接到由 PnP 管理器在初始化时传递给驱动程序的 AddDevice 例程的设备对象。 **IoAttachDeviceToDeviceStack** 将新设备对象附加到设备堆栈的当前顶部。

创建设备对象并将其附加到设备堆栈时无需使用磁带 miniclass、中转换器 miniclass 或 SCSI 微型端口驱动程序。 相反，系统提供的磁带类、更换器类或 SCSI 端口驱动程序代表 miniclass/微型端口处理这些任务，调用 miniclass/微型端口驱动程序例程来收集创建设备对象所需的数据。

存储端口驱动程序创建 (类型 FILE_DEVICE_MASS_STORAGE 的 PDOs) 的物理设备对象。 Disk 类、CD-ROM 类、磁带类和变换器类驱动程序分别创建 FDOs 类型 FILE_DEVICE_DISK、FILE_DEVICE_CD_ROM、FILE_DEVICE_TAPE 和 FILE_DEVICE_CHANGER。

有关设计 PnP 驱动程序的信息，请参阅 [PnP 驱动程序设计指南](../kernel/pnp-driver-design-guidelines.md)。 有关 PnP 相关 **Io**_Xxx_ 例程的信息，请参阅 [即插即用例程](/windows-hardware/drivers/ddi/index)。
