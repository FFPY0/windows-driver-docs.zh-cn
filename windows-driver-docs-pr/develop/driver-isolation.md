---
title: 驱动程序包隔离
description: 此页面介绍了驱动程序隔离，这是 Windows 驱动程序的一项要求。
ms.date: 10/01/2019
ms.localizationpriority: medium
ms.openlocfilehash: 355636f6474ea77d479dcd7cf23e32ccf97bff34
ms.sourcegitcommit: fa9479a73ebbbace04e9cabdf36aa8b1414c1554
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/26/2021
ms.locfileid: "98792683"
---
# <a name="driver-package-isolation"></a>驱动程序包隔离

驱动程序包隔离是 Windows 驱动程序的一项要求，让驱动程序对外部变化更有弹性、更容易更新和安装。

> [!NOTE]
> 尽管驱动程序包隔离是针对 Windows 驱动程序的要求，但 Windows 桌面驱动程序仍可从中受益，因为此要求提高了复原能力和可维护性。

下表在左侧列中显示了 Windows 驱动程序不再允许的旧驱动程序做法，在右侧列中显示了要求的 Windows 驱动程序行为。

|非隔离驱动程序|独立驱动程序|
|-|-|
|INF 将文件复制到 System32\drivers|驱动程序文件从驱动程序存储运行|
|使用硬编码路径与其他驱动程序交互|使用系统提供的功能或设备接口与其他驱动程序交互|
|将路径硬编码到全局注册表位置|使用 HKR 和系统提供的功能获取注册表和文件状态的相对位置|
|运行时文件写入任何位置|驱动程序将文件写入系统提供的位置|


## <a name="run-from-driver-store"></a>从驱动程序存储运行

所有独立驱动程序包都将其驱动程序包文件保留在驱动程序存储中。 这意味着，它们在其 INF 中指定 [DIRID 13](../install/using-dirids.md) 以在安装时指定驱动程序包文件的位置。

从 Windows 10 版本 1803 和更高版本上的 DriverStore 运行的 WDM 或 KMDF 驱动程序应，需要访问其设备驱动程序时，应调用 [IoGetDriverDirectory](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdriverdirectory)，并将 DriverDirectoryImage 设置为目录类型，以获取用于加载驱动程序的目录路径。

或者，对于需要支持 Windows 10 版本 1803 之前的 OS 版本的驱动程序，使用 [IoQueryFullDriverPath](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-ioqueryfulldriverpath) 查找驱动程序的路径，获取用于加载驱动程序的目录路径，并查找相对于该路径的配置文件。  如果内核模式驱动程序是 KMDF 驱动程序，则它可以使用 [**WdfDriverWdmGetDriverObject**](/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdriverwdmgetdriverobject) 来检索要传递到 IoQueryFullDriverPath 的 WDM 驱动程序对象。 UMDF 驱动程序可以使用 [**GetModuleHandleExW**](/windows/win32/api/libloaderapi/nf-libloaderapi-getmodulehandleexw) 和 [**GetModuleFileNameW**](/windows/win32/api/libloaderapi/nf-libloaderapi-getmodulefilenamew) 来确定驱动程序是从何处加载的。  例如：

```cpp
bRet = GetModuleHandleExW(GET_MODULE_HANDLE_EX_FLAG_FROM_ADDRESS,
                         (PCWSTR)&DriverEntry,
                         &handleModule);
if (bRet) {
    charsWritten = GetModuleFileNameW(handleModule,
                                      path,
                                      pathLength);
    …
```

对于 INF 负载的文件，INF 中该文件的 [SourceDisksFiles](../install/inf-sourcedisksfiles-section.md) 条目中列出的 subdir 必须与 INF 中该文件的 [DestinationDirs](../install/inf-destinationdirs-section.md) 条目中列出的 subdir 匹配 。

此外，[CopyFiles](../install/inf-copyfiles-directive.md) 指令不能用于重命名文件。 这些限制是必需的，这样在设备上安装 INF 才不会导致在 DriverStore 目录中创建新文件。

由于 [SourceDisksFiles](../install/inf-sourcedisksfiles-section.md) 条目无法具有多个文件名相同的条目，并且 CopyFiles 不能用于重命名文件，因此 INF 引用的每个文件必须具有唯一的文件名。

### <a name="dynamically-finding-and-loading-files-from-the-driver-store"></a>从驱动程序存储动态查找和加载文件

在某些情况下，驱动程序包可能包含应该由另一驱动程序包中的二进制文件加载或由某个用户模式组件加载的文件。

下面有几个示例：

* 用户模式 DLL 提供一个用来与驱动程序包中的驱动程序通信的接口。
* 扩展驱动程序包包含一个由基准驱动程序包中的驱动程序加载的配置文件。

在这些情况下，驱动程序包应该设置某个状态来指示文件的路径或由设备公开的设备接口。

例如，驱动程序包可以使用 HKR [**AddReg**](../install/inf-addreg-directive.md) 来设置此状态。 在此示例中，应该假定：对于 `ExampleFile.dll`，驱动程序包有一个没有任何 *subdir* 的 [**SourceDisksFiles**](../install/inf-sourcedisksfiles-section.md) 条目。  这样就会将文件置于驱动程序包目录的根目录中，而 [**CopyFiles**](../install/inf-copyfiles-directive.md) 指令的 [**DestinationDirs**](../install/inf-destinationdirs-section.md) 则指定 **dirid** 13。

下面是一个 INF 示例，演示了如何将其设置为设备状态：

```cpp
[ExampleDDInstall.HW]
AddReg = Example_DDInstall.AddReg

[Example_DDInstall.AddReg]
HKR,,ExampleValue,,%13%\ExampleFile.dll
```

而将其设置为设备接口状态的 INF 示例为：

```cpp
[ExampleDDInstall.Interfaces]
AddInterface = {<fill in an interface class GUID for an interface exposed by the device>},,Example_Add_Interface_Section

[Example_Add_Interface_Section]
AddReg = Example_Add_Interface_Section.AddReg

[Example_Add_Interface_Section.AddReg]
HKR,,ExampleValue,,%13%\ExampleFile.dll
```

前面的示例使用空的标志值，这会导致生成 REG_SZ 注册表值。 这样就会将 **%13%** 转换成完全限定的用户模式文件路径。 在许多情况下，最好是将路径设置为某个环境变量的相对值。 如果使用标志值 **0x20000**，则注册表值为类型 REG_EXPAND_SZ，而 **%13%** 则会转换为一个包含相应环境变量的路径，该变量用于抽象路径的位置。 检索此注册表值时，请调用 [**ExpandEnvironmentStrings**](/windows/win32/api/rrascfg/nn-rrascfg-ieapproviderconfig) 来解析路径中的环境变量。

如果此值需由内核模式组件读取，则此值应该是 REG_SZ 值。 内核模式组件在读取该值时应该在其前面预置 `\??\`，然后再将其传递给 [**ZwOpenFile**](/windows-hardware/drivers/ddi/wdm/nf-wdm-zwopenfile) 之类的 API。

当此设置成为设备状态的一部分时，如果要访问它，则应用程序必须先找到设备的标识。  用户模式代码可以使用 [**CM_Get_Device_ID_List_Size**](/windows/win32/api/cfgmgr32/nf-cfgmgr32-cm_get_device_id_list_sizea) 和 [**CM_Get_Device_ID_List**](/windows/win32/api/cfgmgr32/nf-cfgmgr32-cm_get_device_id_lista) 获取设备的列表（按需筛选）。 该设备列表可能包含多个设备，因此请先搜索相应的设备，然后再从设备读取状态。 例如，在查找符合特定条件的设备时，请调用 [**CM_Get_DevNode_Property**](/windows/win32/api/cfgmgr32/nf-cfgmgr32-cm_get_devnode_propertyw) 来检索设备的属性。

找到正确的设备以后，请调用 [**CM_Open_DevNode_Key**](/windows/win32/api/cfgmgr32/nf-cfgmgr32-cm_open_devnode_key) 来获取存储设备状态的注册表位置的句柄。

内核模式代码应该检索 PDO（Physical Device Object，物理设备对象）并调用 [**IoOpenDeviceRegistryKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceregistrykey)。

若要在此设置是设备接口状态时访问它，可以通过用户模式代码来调用 [**CM_Get_Device_Interface_List_Size**](/windows/win32/api/cfgmgr32/nf-cfgmgr32-cm_get_device_interface_list_sizea) 和 [**CM_Get_Device_Interface_List**](/windows/win32/api/cfgmgr32/nf-cfgmgr32-cm_get_device_interface_lista)。

另外，可以使用 [**CM_Register_Notification**](/windows/win32/api/cfgmgr32/nf-cfgmgr32-cm_register_notification) 来获取设备接口的到达和删除通知，这样就可以在启用接口时通知代码，让代码随后检索状态。 在设备接口类（在上述 API 中使用）中可能有多个设备接口。  检查这些接口，确定哪个接口是适合读取设置的接口。

找到正确的设备接口以后，调用 [**CM_Open_Device_Interface_Key**](/windows/win32/api/cfgmgr32/nf-cfgmgr32-cm_open_device_interface_keyw)。

内核模式代码可以检索从其获取状态的设备接口的符号链接名称。 为此，请调用 [**IoRegisterPlugPlayNotification**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterplugplaynotification)，以便注册获取相应设备接口类的设备接口通知。  也可调用 [**IoGetDeviceInterfaces**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceinterfaces)，获取系统中当前设备接口的列表。  在设备接口类（在上述 API 中使用）中可能有多个设备接口。  检查这些接口，确定哪个接口是应该读取设置的正确接口。

找到适当的符号链接名称以后，请调用 [**IoOpenDeviceInterfaceRegistryKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceinterfaceregistrykey)，以便检索在其中存储了设备接口状态的注册表位置的句柄。

> [!NOTE]
> 将 **CM_GETIDLIST_FILTER_PRESENT** 标志与 [CM_Get_Device_ID_List_Size](/windows/win32/api/cfgmgr32/nf-cfgmgr32-cm_get_device_id_list_sizea) 和 [**CM_Get_Device_ID_List**](/windows/win32/api/cfgmgr32/nf-cfgmgr32-cm_get_device_id_lista) 配合使用，或者将 **CM_GET_DEVICE_INTERFACE_LIST_PRESENT** 标志与 [**CM_Get_Device_Interface_List_Size**](/windows/win32/api/cfgmgr32/nf-cfgmgr32-cm_get_device_interface_list_sizew) 和 [**CM_Get_Device_Interface_List**](/windows/win32/api/cfgmgr32/nf-cfgmgr32-cm_get_device_interface_lista) 配合使用。 这样可确保硬件存在并已做好通信准备。


## <a name="using-device-interfaces"></a>使用设备接口

需要在驱动程序之间共享状态时，应该只有一个驱动程序拥有共享状态，并且该驱动程序应该为其他驱动程序提供一种读取和修改该状态的方法 。

通常，拥有该状态的驱动程序会在自定义设备接口类中公开一个设备接口。 当驱动程序准备好让其他驱动程序访问该状态时，它将启用该接口。 其他驱动程序可以注册[设备接口到达通知](../install/registering-for-notification-of-device-interface-arrival-and-device-removal.md)。 要访问状态，自定义设备接口类可以定义两个协议之一：

* I/O 协议，可以与提供访问状态的机制的设备接口类相关联。 其他驱动程序使用已启用的设备接口来发送符合协议的 I/O 请求。
* 直接调用接口通过查询接口返回。 其他驱动程序可以通过发送 [IRP_MN_QUERY_INTERFACE](../kernel/irp-mn-query-interface.md) 从驱动程序检索函数指针以进行调用。

或者，如果拥有该状态的驱动程序允许直接访问该状态，其他驱动程序则可以通过使用系统提供的功能以编程方式访问设备接口状态来访问该状态。

这些接口或状态（取决于使用的共享方法）需要进行正确的版本控制，以便拥有该状态的驱动程序可以独立于访问该状态的其他驱动程序而获得服务。 驱动程序供应商不能同时依赖于正在获得服务且版本相同的两个驱动程序。  

因为控制接口的设备和驱动程序变化不定，所以驱动程序和应用程序应该避免在组件启动时调用 [IoGetDeviceInterfaces](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceinterfaces) 来获取已启用接口的列表。

最佳做法是注册设备接口到达或删除的通知，然后调用适当的函数来获取计算机上现有的已启用接口的列表。

有关设备接口的详细信息，请参阅：

* [使用设备接口](../wdf/using-device-interfaces.md)
* [注册获取设备接口到达和设备删除通知](../install/registering-for-notification-of-device-interface-arrival-and-device-removal.md)
* [注册设备接口更改通知](../kernel/registering-for-device-interface-change-notification.md)

## <a name="reading-and-writing-state"></a>读取和写入状态

> [!NOTE]
> 如果组件使用的是设备或设备接口属性来存储状态，则继续使用该方法和适当的 OS API 来存储并访问状态。 以下指南适用于需要由组件存储的其他状态。

对各种状态的访问应该通过调用函数来完成，这些函数向调用方提供状态的位置，然后系统将读取/写入与该位置相关的状态。 请勿使用硬编码的绝对注册表路径和文件路径。

本节包含以下小节：

* [PnP 设备注册表状态](#pnp-device-registry-state)
* [设备接口注册表状态](#device-interface-registry-state)
* [服务注册表状态](#service-registry-state)
* [设备文件状态](#device-file-state)
* [服务文件状态](#service-file-state)

### <a name="pnp-device-registry-state"></a>PnP 设备注册表状态

独立驱动程序包和用户模式组件通常使用两个位置在注册表中存储设备状态。 它们是用于设备的硬件密钥（设备密钥）和用于设备的软件密钥（驱动程序密钥） 。 若要检索这些注册表位置的句柄，请根据使用的平台使用以下选项之一：


* [**IoOpenDeviceRegistryKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceregistrykey) (WDM)
* [**WdfDeviceOpenRegistryKey**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceopenregistrykey)、[**WdfFdoInitOpenRegistryKey**](/windows-hardware/drivers/ddi/wdffdo/nf-wdffdo-wdffdoinitopenregistrykey) (WDF)
* [**CM_Open_DevNode_Key**](/windows/win32/api/cfgmgr32/nf-cfgmgr32-cm_open_devnode_key)（用户模式代码）
* [**INF AddReg**](../install/inf-addreg-directive.md) 指令，使用引用自 [INF DDInstall](../install/inf-ddinstall-section.md) 部分或 [DDInstall.HW](../install/inf-ddinstall-hw-section.md) 部分的 add-registry-section 中的 HKR reg-root 条目，如下所示：

```
[ExampleDDInstall.HW]
AddReg = Example_DDInstall.AddReg

[Example_DDInstall.AddReg] 
HKR,,ExampleValue,,%13%\ExampleFile.dll
```
### <a name="device-interface-registry-state"></a>设备接口注册表状态

使用设备接口与其他驱动程序和组件共享状态。 请勿将路径硬编码到全局注册表位置。

若要读取和写入设备接口注册表状态，请根据使用的平台使用以下选项之一：

* [**IoOpenDeviceInterfaceRegistryKey**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceinterfaceregistrykey) (WDM) 
* [**CM_Open_Device_Interface_Key**](/windows/win32/api/cfgmgr32/nf-cfgmgr32-cm_open_device_interface_keyw)（用户模式代码）
* [INF AddReg](../install/inf-addreg-directive.md) 指令，使用引用自 [add-interface-section](../install/inf-addinterface-directive.md) 部分的 add-registry-section 中的 HKR reg-root 条目 

### <a name="service-registry-state"></a>服务注册表状态

INF 为驱动程序和 Win32 服务设置的注册表值应存储在服务的“参数”子项下，方法是在 [AddReg](../install/inf-addreg-directive.md) 部分中提供 HKR 行，然后在 INF 的服务安装部分引用该部分。  例如：

```
[ExampleDDInstall.Services]
Addservice = ExampleService, 0x2, Example_Service_Inst

[Example_Service_Inst]
DisplayName    = %ExampleService.SvcDesc%
ServiceType    = 1
StartType      = 3
ErrorControl   = 1
ServiceBinary  = %13%\ExampleService.sys
AddReg=Example_Service_Inst.AddReg

[Example_Service_Inst.AddReg]
HKR, Parameters, ExampleValue, 0x00010001, 1
```

若要访问该状态的位置，请根据平台使用下列函数之一：

* [IoOpenDriverRegistryKey](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendriverregistrykey) (WDM)，DRIVER_REGKEY_TYPE 为 DriverRegKeyParameters
* [**WdfDriverOpenParametersRegistryKey**](/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdriveropenparametersregistrykey) (WDF)
* [GetServiceRegistryStateKey](/windows/win32/api/winsvc/nf-winsvc-getserviceregistrystatekey)（Win32 服务），SERVICE_REGISTRY_STATE_TYPE 为 ServiceRegistryStateParameters

这些由 INF 在服务的“参数”子键中提供的注册表值不应该在运行时修改，应视为只读的值。  在运行时写入的注册表值应在不同的位置下写入。  若要访问要在运行时写入的状态的位置，请使用以下函数之一：

* [IoOpenDriverRegistryKey](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendriverregistrykey) (WDM)，DRIVER_REGKEY_TYPE 为 DriverRegKeyPersistentState
* [WdfDriverOpenPersistentStateRegistryKey](/windows-hardware/drivers/ddi/wdfdriver/nf-wdfdriver-wdfdriveropenpersistentstateregistrykey) (WDF)
* [GetServiceRegistryStateKey](/windows/win32/api/winsvc/nf-winsvc-getserviceregistrystatekey)（Win32 服务），SERVICE_REGISTRY_STATE_TYPE 为 ServiceRegistryStatePersistent

### <a name="device-file-state"></a>设备文件状态

如果需要写入与设备相关的文件，这些文件应相对于通过 OS API 提供的句柄或文件路径进行存储。 例如，特定于该设备的配置文件就是一个应存储在此处的文件类型。

* [IoGetDeviceDirectory](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdevicedirectory) (WDM)，DirectoryType 参数设置为 DeviceDirectoryData  
* [**WdfDeviceRetrieveDeviceDirectoryString**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceretrievedevicedirectorystring) (WDF)

### <a name="service-file-state"></a>服务文件状态

Win32 和驱动程序服务均读取和写入关于本身的状态。

若要访问服务自己的内部状态值，该服务需使用下列选项之一： 

* [IoGetDriverDirectory](/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdriverdirectory) (WDM)，DirectoryType 参数设置为 DeviceDirectoryData  
* [IoGetDriverDirectory](/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iogetdriverdirectory) (KMDF)，DirectoryType 参数设置为 DeviceDirectoryData  
* [**WdfDriverRetrieveDriverDataDirectoryString**](/windows-hardware/drivers/ddi/content/wdfdriver/nf-wdfdriver-wdfdriverretrievedriverdatadirectorystring) (UMDF)
* [GetServiceDirectory](/windows/win32/api/winsvc/nf-winsvc-getservicedirectory)（Win32 服务），eDirectoryType 参数设置为 ServiceDirectoryPersistentState  

若要与其他组件共享服务的内部状态，请使用受控制的、受版本控制的接口，而不是直接注册表或文件读取。

## <a name="driverdata-and-programdata"></a>DriverData 和 ProgramData

用作可与其他组件共享的中间操作的一部分的文件应该写入 DriverData 或 ProgramData 位置 。

这些位置为组件提供一个位置，用于写入临时状态或旨在由其他组件使用、可能从某一系统收集和复制以供另一系统处理的状态。  例如，自定义日志文件或故障转储符合此描述。

避免在 `DriverData` 或 `ProgramData` 目录的根目录中写入文件。 请改用公司名称创建子目录，然后在在该目录中写入文件和更多子目录。

例如，对于 Contoso 的公司名称，内核模式驱动程序可将自定义日志写入 `\DriverData\Contoso\Logs`，用户模式应用程序可收集或分析 `%DriverData%\Contoso\Logs` 中的日志文件。

### <a name="driverdata"></a>DriverData

Windows 10 版本 1803 及更高版本中提供了 `DriverData` 目录，可供管理员和 UMDF 驱动程序访问。

内核模式驱动程序使用系统提供的名为 `\DriverData` 的符号链接访问 `DriverData` 目录。
用户模式程序使用环境变量 `%DriverData%` 访问 `DriverData` 目录。

### <a name="programdata"></a>ProgramData

`%ProgramData%` 用户模式环境变量适用于存储数据时要使用的用户模式组件。 

