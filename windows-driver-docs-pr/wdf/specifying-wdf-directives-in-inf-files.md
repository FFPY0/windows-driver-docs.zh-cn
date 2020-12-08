---
title: 在 INF 文件中指定 WDF 指令
description: 在 INF 文件中指定 WDF 指令
keywords:
- WDF 指令 WDK UMDF
- DDInstall 部分 WDK UMDF
- UmdfService INF 指令 WDK UMDF
- UmdfServiceOrder INF 指令 WDK UMDF
- UmdfImpersonationLevel INF 指令 WDK UMDF
- UmdfMethodNeitherAction INF 指令 WDK UMDF
- UmdfKernelModeClientPolicy INF 指令 WDK UMDF
- UmdfLibraryVersion INF 指令 WDK UMDF
- ServiceBinary INF 指令 WDK UMDF
- DriverCLSID INF 指令 WDK UMDF
- 指令 WDK UMDF
- 特定于 UMDF 的指令 WDK
- UMDF-服务-安装部分 WDK
- INF 文件 WDK UMDF，指令
- UmdfDispatcher INF 指令 WDK UMDF，语法
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 14e8dabea93d17274218b589c5c32edb38ee84b0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96821135"
---
# <a name="specifying-wdf-directives-in-inf-files"></a>在 INF 文件中指定 WDF 指令


本主题适用于 User-Mode Driver Framework (UMDF) 版本1和2。

安装 UMDF 驱动程序的 INF 文件必须包含 Microsoft Windows 驱动程序框架 (WDF) 特定的 *DDInstall* 部分。 如果 INF 文件安装多个 WDF 驱动程序，则 INF 文件可以包含多个 WDF 特定的 *DDInstall* 部分。 每个 WDF 特定的 *DDInstall* 部分：

-   对应于与特定 WDF 驱动程序关联的 [**DDInstall**](../install/inf-ddinstall-section.md) 和 [**DDInstall**](../install/inf-ddinstall-services-section.md) 节。

-   所有已加载的 WDF 共同安装程序都将对其进行处理，该程序以任意顺序运行。

-   包含设备的 WDF 安装指令。 UMDF 特定指令以 UMDF 前缀开头，KMDF 特定指令以 KMDF 前缀开头。

下面的代码示例显示特定于 WDF 的 *DDInstall* 部分中的特定于 UMDF 的指令。

```cpp
[Skeleton_Install.Wdf]
UmdfService=UMDFSkeleton,UMDFSkeleton_Install
UmdfServiceOrder=UMDFSkeleton
```

此页介绍了特定于 WDF 的 *DDInstall* 部分中的每个 UMDF 特定指令。 您可以使用此文章中的链接在指令之间导航。

## <a name="umdfservice"></a>UmdfService

`**UmdfService** = <*serviceName*>，<*sectionName*>

将一个 UMDF 驱动程序与一个包含安装 UMDF 驱动程序所需的信息的 *umdf 服务安装* 部分关联。 *ServiceName* 参数指定 UMDF 驱动程序，且长度限制为最多31个字符。 *SectionName* 参数引用 *UMDF-service 安装* 部分。 有效的 INF 文件通常至少需要一个 **UmdfService** 指令。 但是，如果一个 UMDF 驱动程序是操作系统的一部分，则不需要为 UMDF 驱动程序使用 **UmdfService** 指令。 因此，尽管大多数 INF 文件都有针对每个 UMDF 驱动程序的 **UmdfService** 指令，但有效 inf 文件可能没有任何 **UmdfService** 指令。

## <a name="umdfhostprocesssharing"></a>UmdfHostProcessSharing

*此指令在 UMDF 版本1.11 及更高版本中受支持。*

**UmdfHostProcessSharing** = <**ProcessSharingDisabled**  |  **ProcessSharingEnabled**>


确定是否将设备堆栈置于共享进程池中 (**ProcessSharingEnabled**) 或 (**ProcessSharingDisabled**) 的单独进程。 默认值为 **ProcessSharingEnabled**。 此指令特定于设备，而不是特定于驱动程序。

有关设备池的详细信息，请参阅 [在 UMDF 驱动程序中使用设备池](using-device-pooling-in-umdf-drivers.md)。


## <a name="umdfdirecthardwareaccess"></a>UmdfDirectHardwareAccess

*此指令在 UMDF 版本1.11 及更高版本中受支持。*

**UmdfDirectHardwareAccess** = <**AllowDirectHardwareAccess**  |  **RejectDirectHardwareAccess**> 

指示框架是否应允许驱动程序使用任何直接的硬件访问功能，如访问设备寄存器和端口、扫描分配给设备的硬件资源、处理硬件中断或获取连接资源。

如果 **UmdfDirectHardwareAccess** 设置为 **AllowDirectHardwareAccess**，则该框架允许驱动程序使用执行直接硬件访问的 UMDF 接口。

如果 UMDF 驱动程序访问硬件资源（如寄存器或端口、中断、[常规用途 i/o](../gpio/gpio-driver-support-overview.md) (GPIO) 引脚或串行总线连接，例如 I2C、SPI 和串行端口），则必须指定 **AllowDirectHardwareAccess** 。 驱动程序通过其 [*EvtDevicePrepareHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)回调函数的 *ResourcesRaw* 和 *ResourcesTranslated* 参数接收所有这些资源。

> [!NOTE]
> 从 UMDF 版本2.15 开始，UMDF 驱动程序无需指定 **AllowDirectHardwareAccess** 即可在其 [*EvtDevicePrepareHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware) 回调例程中接收硬件资源列表。 如果未指定此项，则驱动程序将不具有使用这些资源的访问权限，但有一个例外：如果为设备分配了一个或多个 (**CmResourceTypeConnection** 的连接资源) 和一个或多个中断资源 (**CmResourceTypeInterrupt**) ，则驱动程序可以从其 [*EvtDevicePrepareHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)回调例程 (而不是从 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)) 调用 [**WdfInterruptCreate**](/windows-hardware/drivers/ddi/wdfinterrupt/nf-wdfinterrupt-wdfinterruptcreate) 。

 

有关将 UMDF 驱动程序连接到特定类型的资源的信息，请参阅：

-   [用户模式 SPB 外设驱动程序的硬件资源](../spb/hardware-resources-for-user-mode-spb-peripheral-drivers.md)
-   [SPB 连接的外围设备的连接 ID](../spb/connection-ids-for-spb-connected-peripheral-devices.md)
-   [将 UMDF 外设驱动程序连接到串行端口](/previous-versions/hh406559(v=vs.85))

如果 **UmdfDirectHardwareAccess** 设置为 **RejectDirectHardwareAccess**，则框架不允许驱动程序使用任何直接的硬件访问功能。 默认值为 **RejectDirectHardwareAccess**。

有关 UMDF 驱动程序如何访问硬件资源的信息，请参阅 [查找和映射硬件资源](finding-and-mapping-hardware-resources.md)。


## <a name="umdfhostpriority"></a>UmdfHostPriority

*此指令在 UMDF 版本2.15 及更高版本中受支持。*

**UmdfHostPriority** = <**PriorityHigh**>  

UMDF HID 客户端驱动程序可以将 **UmdfHostPriority** 设置为 **PriorityHigh** ，以提高其线程优先级。 此指令只应用于对用户响应时间敏感的触摸或输入驱动程序。 当驱动程序指定 **PriorityHigh** 时，系统会将其放在单独的设备池中，并与其他具有相似优先级的驱动程序一起使用。 由于其他设备池使用的内存更多，因此应谨慎使用此设置。 有关设备池的详细信息，请参阅 [在 UMDF 驱动程序中使用设备池](using-device-pooling-in-umdf-drivers.md)。

## <a name="umdfregisteraccessmode"></a>UmdfRegisterAccessMode

*此指令在 UMDF 版本1.11 及更高版本中受支持。*

**UmdfRegisterAccessMode** = <**RegisterAccessUsingSystemCall**  |  **RegisterAccessUsingUserModeMapping**>   

指示框架是否应将寄存器映射到用户模式地址空间 (以便在访问寄存器) 时不涉及系统调用，或使用系统调用来访问寄存器。

如果 **UmdfRegisterAccessMode** 设置为 **RegisterAccessUsingSystemCall**，则框架将使用系统调用来访问寄存器。

如果将 **UmdfRegisterAccessMode** 设置为 **RegisterAccessUsingUserModeMapping**，则框架会将寄存器映射到用户模式地址空间，以便不需要系统调用即可访问寄存器。 默认值为 **RegisterAccessUsingSystemCall**。


##  <a name="umdfserviceorder"></a>UmdfServiceOrder

**UmdfServiceOrder** = <*serviceName1* >  \[ ，<*serviceName2*> .。。\]  

列出共同安装程序在设备堆栈上安装 UMDF 驱动程序的顺序。 即使共同安装程序在设备堆栈上只安装一个 UMDF 驱动程序，INF 文件也必须包含此指令。 *ServiceNameXx* 参数对应于每个 **UmdfService** 指令的 *serviceName* 参数。 因为 UMDF 驱动程序会按照它们列出的顺序添加到设备堆栈中，所以第一个参数指定设备堆栈中最低的 UMDF 驱动程序。

若要确保 UMDF 共同安装程序安装设备，任何给定的特定于 WDF 的 *DDInstall* 节中都必须有一个 **UmdfServiceOrder** 指令。 也就是说，不能使用 "**包括**" 和 "**需要**" 指令导入 **UmdfServiceOrder** 指令。

## <a name="umdfimpersonationlevel"></a>UmdfImpersonationLevel

**UmdfImpersonationLevel** = <*级别*>  

通知框架有关 UMDF 驱动程序可以具有的最大模拟级别。 **UmdfImpersonationLevel** 指令是可选的;如果未指定模拟级别，则默认值为 "**标识**"。 当应用程序打开文件句柄时，应用程序可以向该驱动程序授予更高的模拟级别。 但是，驱动程序无法调用 [**IWDFIoRequest：：模拟**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iwdfiorequest-impersonate) 方法来请求大于 **UmdfImpersonationLevel** 指定的级别的模拟级别。 此指令的可能值为：

-   **匿名**

-   **标识**

-   **模拟**

-   **委托**

这些值与 [**安全 \_ 模拟 \_ 级别**](/windows-hardware/drivers/ddi/wudfddi/ne-wudfddi-_security_impersonation_level) 枚举中指定的值相对应。

## <a name="umdfmethodneitheraction"></a>UmdfMethodNeitherAction

**UmdfMethodNeitherAction** = <**副本**  |  **拒绝**>  

指示框架是否将接受 (**复制**) 或拒绝 () **拒绝** 设备的 i/o 请求，如果请求对象包含指定方法的 i/o 控制代码 [ \_ 不](../kernel/buffer-descriptions-for-i-o-control-codes.md) 是缓冲区访问方法，则为。 **UmdfMethodNeitherAction** 指令是可选的。 如果未指定指令，则默认值为 " **拒绝**"。

有关支持方法的详细信息 \_ ，请参阅基于 umdf 的驱动程序中的 "不 [使用缓冲的 i/o" 和 "直接](./accessing-data-buffers-in-umdf-1-x-drivers.md#using-neither-buffered-i-o-nor-direct-i-o-in-umdf-drivers)i/o"。

## <a name="umdfdispatcher"></a>UmdfDispatcher

**UmdfDispatcher** = <**FileHandle**  |  **WinUsb**  |  **NativeUSB**>  

通知框架在设备堆栈的用户模式部分进行 i/o 后，要将 i/o 发送到何处。 默认情况下，会将 i/o 发送到反射器 ( # A0) 。 通过将 **UmdfDispatcher** 设置为 **WinUsb**，驱动程序指示 UMDF 将 i/o 发送到 WinUsb 体系结构。 从 UMDF 2.15 开始，指定 **NativeUSB** 会导致反射器处理 USB i/o。

-   如果堆栈中的任何驱动程序使用基于文件句柄的目标，请将此指令设置为 **FileHandle**。
-   如果驱动程序使用 UMDF 2.15 或更高版本并使用 USB i/o 目标，则将此指令设置为 **NativeUSB**。
-   如果驱动程序使用的是 UMDF 2.15，并使用 USB i/o 目标，则将此指令设置为 **WinUsb**。

**UmdfDispatcher** 指令是可选的。

下面的代码示例显示特定于 WDF 的 **DDInstall** 部分中的 **UmdfDispatcher** 指令。

```cpp
[Xxx_Install.Wdf]
UmdfDispatcher=NativeUSB
```

## <a name="umdfkernelmodeclientpolicy"></a>UmdfKernelModeClientPolicy

*此指令在 UMDF 版本1.9 及更高版本中受支持。*

**UmdfKernelModeClientPolicy** = <**AllowKernelModeClients**  |  **RejectKernelModeClients**>  

若要允许将内核模式驱动程序加载到早期 UMDF 版本中的用户模式驱动程序之上，请参阅 [早期 Umdf 版本中的内核模式客户端支持](./supporting-kernel-mode-clients-in-umdf-1-x-drivers.md#kernel-mode-client-support-in-earlier-umdf-versions)。

指示框架是否应允许驱动程序接收来自内核模式驱动程序的 i/o 请求。

如果将 **UmdfKernelModeClientPolicy** 设置为 **AllowKernelModeClients**，则框架允许将内核模式驱动程序加载到用户模式驱动程序之上，并将来自内核模式驱动程序的 i/o 请求传递到用户模式驱动程序。

如果将 **UmdfKernelModeClientPolicy** 设置为 **RejectKernelModeClients**，则框架不允许将内核模式驱动程序加载到用户模式驱动程序之上，并且它不会将任何内核模式驱动程序的 i/o 请求传递到用户模式驱动程序。 如果驱动程序的 INF 文件不包含此指令，则默认值为 **RejectKernelModeClients**。 有关详细信息，请参阅 [支持内核模式客户端](./supporting-kernel-mode-clients-in-umdf-1-x-drivers.md)。


## <a name="umdffileobjectpolicy"></a>UmdfFileObjectPolicy

*此指令在 UMDF 版本1.11 及更高版本中受支持。*

**UmdfFileObjectPolicy** = <**RejectNullAndUnknownFileObjects**  |  **AllowNullAndUnknownFileObjects**>   

指示框架是否应允许处理 ([IWDFIoRequest](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiorequest)) 的 i/o 请求，这些请求要么不与 ([IWDFFile](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdffile)) 的文件对象相关联，要么与未知文件对象关联， (某个文件对象的驱动程序以前未看到其 create 请求) 。

如果 **UmdfFileObjectPolicy** 设置为 **RejectNullAndUnknownFileObjects**，则框架不允许处理与 NULL 或未知文件对象关联的请求。

如果 **UmdfFileObjectPolicy** 设置为 **AllowNullAndUnknownFileObjects**，则框架允许处理与 NULL 或未知文件对象关联的请求。

默认值为 **RejectNullAndUnknownFileObjects**。


## <a name="umdffscontextusepolicy"></a>UmdfFsContextUsePolicy

*此指令在 UMDF 版本1.11 及更高版本中受支持。*

**UmdfFsContextUsePolicy** = <**CanUseFsContext**  |  **CanUseFsContext2**  |  **CannotUseFsContexts**> 

指示框架是否可以在 WDM 文件对象的特定上下文成员中存储内部信息。 如果同一堆栈中的内核模式驱动程序使用文件对象的特定成员，则可以使用此指令请求该框架不使用同一位置。

如果将 **UmdfFsContextUsePolicy** 设置为 **CanUseFsContext**，则框架会将信息存储在 WDM 文件对象的 **FsContext** 成员中。

如果将 **UmdfFsContextUsePolicy** 设置为 **CanUseFsContext2**，则框架会将信息存储在 WDM 文件对象的 **FsContext2** 成员中。

如果 **UmdfFsContextUsePolicy** 设置为 **CannotUseFsContexts**，则框架不使用 **FsContext** 或 **FsContext2**。

默认值为 **CanUseFsContext**。


下面的代码示例演示了一个 " *UMDF-服务-安装* " 一节中所需的指令。

```cpp
[UMDFSkeleton_Install]
UmdfLibraryVersion=1.0.0
ServiceBinary=%12%\UMDF\UMDFSkeleton.dll
DriverCLSID={d4112073-d09b-458f-a5aa-35ef21eef5de}
```

以下列表介绍了 " *UMDF-服务-安装* " 一节中的每个指令：

## <a name="umdflibraryversion"></a>UmdfLibraryVersion

**UmdfLibraryVersion** = <*版本*>  

向共同安装程序通知 UMDF 驱动程序将使用的框架的版本号。 *版本* 字符串的格式 <*主要*>。 <*次*> <*服务*。 当设备堆栈上的驱动程序使用多个版本的 framework 时，INF 文件会将多个共同安装程序（每个 framework 版本）复制到硬盘驱动器上的同一位置。 但 INF 文件仅将最高版本的共同安装程序添加到 **CoInstallers32** 注册表值。 有关复制共同安装程序的详细信息，请参阅 [使用 UMDF 共同安装程序](using-the-umdf-co-installer.md)。

共同安装程序将验证版本字符串，并使用它来找到 UMDF 驱动程序的特定于版本的共同安装程序。 然后，共同安装程序将从特定版本的共同安装程序中提取框架。

## <a name="servicebinary"></a>ServiceBinary

**ServiceBinary** = <*binarypath*>  

通知 UMDF 有关将 UMDF 驱动程序二进制放置在硬盘驱动器上的位置。

应将 UMDF 驱动程序复制到目录，并从目录中运行 `Windows\System32\Drivers\UMDF` 。

## <a name="driverclsid"></a>DriverCLSID

**注意**  仅在1.x 版本中支持此指令。

**DriverCLSID** = < {*CLSID*} >  

通知 UMDF 驱动程序的类标识符 (CLSID) 。 当 UMDF 加载 UMDF 驱动程序时，UMDF 主机使用 UMDF 驱动程序的 CLSID 来创建 UMDF 驱动程序的 [IDriverEntry](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-idriverentry) 接口的实例。

## <a name="umdfextensions"></a>UmdfExtensions

**UmdfExtensions** = <*cxServiceName*>  

对于与 Microsoft 提供的类扩展驱动程序通信的驱动程序是必需的。  CxServiceName 参数对应于与类扩展驱动程序二进制文件关联的服务。

类扩展驱动程序的服务名称可以位于以下注册表项下的子项中： **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\WUDF\Services**
