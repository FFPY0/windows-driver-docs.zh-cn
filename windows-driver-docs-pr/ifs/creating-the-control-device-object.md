---
title: 创建控制设备对象
description: 创建控制设备对象
keywords:
- 控制设备对象 WDK 文件系统
- CDOs WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8e1636d6b8dd4ffa55d41d4fca94c4b2ed67b4bb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837275"
---
# <a name="creating-the-control-device-object"></a>创建控制设备对象


## <span id="ddk_creating_the_control_device_object_if"></span><span id="DDK_CREATING_THE_CONTROL_DEVICE_OBJECT_IF"></span>


文件系统筛选器驱动程序的 [**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 例程通常是通过创建 *控制设备对象* 开始的。 控制设备对象的用途是允许应用程序直接与筛选器驱动程序通信，甚至在筛选器附加到文件系统或卷设备对象之前。

请注意，文件系统还会创建控制设备对象。 当文件系统筛选器驱动程序将自身附加到文件系统而不是单个文件系统卷时，它会将自身附加到文件系统的控制设备对象。

下面的示例创建一个控制设备对象：

```cpp
RtlInitUnicodeString(&nameString, MYLEGACYFILTER_FULLDEVICE_NAME);
status = IoCreateDevice(
        DriverObject,                  //DriverObject
        0,                             //DeviceExtensionSize
        &nameString,                   //DeviceName
        FILE_DEVICE_DISK_FILE_SYSTEM,  //DeviceType
        FILE_DEVICE_SECURE_OPEN,       //DeviceCharacteristics
        FALSE,                         //Exclusive
        &gControlDeviceObject);        //DeviceObject

RtlInitUnicodeString(&linkString, MYLEGACYFILTER_DOSDEVICE_NAME);
status = IoCreateSymbolicLink(&linkString, &nameString);
```

与文件系统不同，文件系统筛选器驱动程序不需要命名其控制设备对象。 由于对 [**IoRegisterDeviceInterface**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterdeviceinterface) 的调用对于控制设备对象无效，用户模式应用程序无法访问具有设备名称的筛选器驱动程序。 如果在 *DeviceName* 参数中传递非 **NULL** 值，则此值将成为控制设备对象的名称。 然后， [**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 例程可以调用 [**IoCreateSymbolicLink**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatesymboliclink) 例程（如前面的代码示例所示），将该对象的内核模式名称链接到对应用程序可见的用户模式名称。

**注意**  控制设备对象是唯一可安全命名的设备对象类型，因为它是未连接到驱动程序堆栈的唯一设备对象。 因此，可以选择性地命名文件系统筛选器驱动程序的控制设备对象。 请注意，必须为文件系统的控制设备对象命名。 不应将筛选器设备对象命名为。

 

分配给 *DeviceType* 参数的值应为 ntifs 中定义的设备类型之一，如 "文件 \_ 设备 \_ 磁盘 \_ 文件 \_ 系统"。

如果在 *DeviceName* 参数中传递了一个非 **NULL** 值，则 *DeviceCharacteristics* 标志必须包含 \_ \_ 打开的文件设备安全 \_ 。 此标志指示 i/o 管理器对发送到控制设备对象的所有打开的请求执行安全检查。 这些安全检查针对命名设备对象的 ACL 进行。

文件系统筛选器驱动程序在调度例程中标识自己的控制设备对象的一种有效方法是将设备指针和以前存储的全局指针与控件设备对象进行比较。 因此，上面的示例将 [**IoCreateDevice**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocreatedevice)返回的 *DeviceObject* 指针存储到 `gControlDeviceObject` 全局定义的指针变量中。

 

