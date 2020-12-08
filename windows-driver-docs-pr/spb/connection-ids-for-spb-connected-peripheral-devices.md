---
title: SPB 连接的外围设备的连接 ID
description: 驱动程序可以将 i/o 请求发送到简单外围总线上的外围设备 (SPB) 中，驱动程序必须打开与设备的逻辑连接。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8cc65ccaec188b7d4e8d88d218c7b24ed69c6a1a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811851"
---
# <a name="connection-ids-for-spb-connected-peripheral-devices"></a>SPB 连接的外围设备的连接 ID


驱动程序可以将 i/o 请求发送到 [简单外围总线](/previous-versions/hh450903(v=vs.85)) 上的外围设备 (SPB) 中，驱动程序必须打开与设备的逻辑连接。 通过此连接，驱动程序可以发送读写请求，以便将数据传入和传出设备。 此外，驱动程序可以将 (IOCTL) 请求的 i/o 控制发送到设备，以便执行特定于 SPB 的操作。




系统启动时，即插即用 (PnP) manager 将同时枚举 PnP 设备和非 PnP 设备。 对于具有与 SPB 的固定连接的非 PnP 外围设备，PnP 管理器会查询硬件平台的 ACPI 固件，以获取描述如何访问设备的一组连接参数。 这些连接参数标识设备连接到的总线的 SPB 控制器，并包含控制器与设备通信所需的其他信息（如总线地址和总线时钟频率）。

PnP 管理器将标识符（称为 *连接 ID*）分配给连接到 SPB 的外围设备的连接参数。 PnP 管理器将此 ID 和连接参数一起存储在名为 *资源中心* 的系统数据存储中。  (资源中心是一种内部数据存储，其中 PnP 管理器存储与 SPB 连接的外围设备有关的配置信息。 ) 连接 ID 封装这些参数，以便驱动程序无需显式提供这些参数。

与 SPB 连接的外围设备的驱动程序将接收设备的连接 ID 作为驱动程序的已分配硬件资源的一部分。 当外围设备的驱动程序调用系统函数以打开与设备的连接时，驱动程序会提供连接 ID，该 ID 用于从资源中心检索设备的连接参数。

驱动程序开发人员可以使用 [用户模式驱动程序框架](../wdf/overview-of-the-umdf.md) (UMDF) 或 [内核模式驱动程序框架](../wdf/index.md) (KMDF) 来构建连接到 SPB 的外围设备的驱动程序。 UMDF 驱动程序会接收其资源 (其中包括连接 ID) 在框架调用驱动程序的 [**IPnpCallbackHardware2：： OnPrepareHardware**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware-onpreparehardware) 方法时）。 KMDF 驱动程序在 [*EvtDevicePrepareHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware) 回调期间接收其硬件资源。

要使 UMDF 外设驱动程序能够在其资源列表中接收连接 Id，安装驱动程序的 INF 文件必须在其特定于 WDF 的 **DDInstall** 节中包含以下指令：

**UmdfDirectHardwareAccess = AllowDirectHardwareAccess** 有关此指令的详细信息，请参阅 [在 INF 文件中指定 WDF 指令](../wdf/specifying-wdf-directives-in-inf-files.md)。 有关 INX 文件的示例， (用于生成使用此指令的相应 INF 文件) ，请参阅 [SpbAccelerometer](https://go.microsoft.com/fwlink/p/?LinkId=618052) 驱动程序示例。

驱动程序作为资源接收的连接 ID 是64位整数，但驱动程序必须将此 ID 合并为可用于从资源中心检索连接参数的设备路径名称。 若要创建设备路径名称，驱动程序将调用 **资源 \_ 中心 \_ \_ \_ 从 \_ ID 函数创建路径** ，该函数是在 Reshub 头文件中声明的。

若要打开与 SPB 连接的外围设备的逻辑连接，UMDF 驱动程序将调用 [**IWDFRemoteTarget：： OpenFileByName**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfremotetarget-openfilebyname) 方法，而 KMDF 驱动程序调用 [**WdfIoTargetOpen**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetopen) 方法。 任一方法都需要设备路径名称作为输入参数。

有关使用连接 Id 打开与 SPB 连接的外围设备的逻辑连接的 UMDF 和 KMDF 代码示例，请参阅以下主题：

[User-Mode SPB 外设驱动程序](./hardware-resources-for-user-mode-spb-peripheral-drivers.md) 
 的硬件资源[Kernel-Mode SPB 外设驱动程序的硬件资源](./hardware-resources-for-kernel-mode-spb-peripheral-drivers.md)用户模式应用程序无法打开到 SPB 连接的外围设备的逻辑连接，并且无法将 i/o 请求直接发送到这些设备。

一次只能有一个驱动程序可以对连接到 SPB 的外围设备保持开放的逻辑连接。 另一个驱动程序尝试打开与同一设备的第二个连接失败。

 

