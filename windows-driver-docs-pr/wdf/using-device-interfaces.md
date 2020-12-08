---
title: '使用设备接口 (WDF) '
description: 使用设备接口
keywords:
- 设备接口 WDK KMDF
- 注册设备接口 WDK KMDF
- 接收设备接口访问请求 WDK KMDF
- 设备接口类 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ca60937ce5c98bbc5ba41704aad613ee1cb794c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840231"
---
# <a name="using-device-interfaces-wdf"></a>使用设备接口 (WDF) 





*设备接口* 是应用程序可用于访问设备即插即用 (PnP) 设备的符号链接。 用户模式应用程序可将接口的符号链接名称传递到 API 元素，例如 Microsoft Win32 **CreateFile** 函数。 若要获取设备接口的符号链接名称，用户模式应用程序可以调用 **SetupDi** 函数。 有关 **SetupDi** 函数的详细信息，请参阅 [使用设备安装函数](../install/using-device-installation-functions.md)。

每个设备接口属于一个 *设备接口类*。 例如，cd-rom 设备的驱动程序堆栈可能提供属于 GUID \_ DEVINTERFACE \_ CDROM 类的接口。 Cd-rom 设备的驱动程序之一将注册 GUID \_ DEVINTERFACE CDROM 类的实例， \_ 以通知系统和应用程序提供 cd-rom 设备。 有关设备接口类的详细信息，请参阅 [设备接口类概述](../install/overview-of-device-interface-classes.md)。

### <a name="registering-a-device-interface"></a>注册设备接口

若要注册设备接口类的实例，基于框架的驱动程序可以从其 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数中调用 [**WdfDeviceCreateDeviceInterface**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreatedeviceinterface) 。 如果驱动程序支持多个接口实例，则可以为每个实例分配一个唯一的引用字符串。

驱动程序注册设备接口后，驱动程序可以调用 [**WdfDeviceRetrieveDeviceInterfaceString**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceretrievedeviceinterfacestring) 来获取系统已分配给设备接口的符号链接名称。

有关驱动程序可以注册设备接口的其他方法的信息，请参阅 [注册设备接口类](../install/registering-a-device-interface-class.md)。

### <a name="enabling-and-disabling-a-device-interface"></a>启用和禁用设备接口

在驱动程序从 [*EVT_WDF_DRIVER_DEVICE_ADD*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)调用 [**WdfDeviceCreateDeviceInterface**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreatedeviceinterface)后，当设备通过 pnp 枚举时，框架会自动启用所有设备的接口，并在设备执行 pnp 删除时禁用接口。 

请注意，任何设备电源状态更改或 PnP 资源重新平衡不会更改接口的状态。 若要防止在 PnP 开始期间自动启用接口，请调用 [**WdfDeviceSetDeviceInterfaceStateEx**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetdeviceinterfacestateex) (将该接口的 *EnableInterface* 参数设置为 FALSE) 。 
 
设备启动后创建的接口不会自动启用。 驱动程序必须调用 [**WdfDeviceSetDeviceInterfaceState**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetdeviceinterfacestate) 或 [**WdfDeviceSetDeviceInterfaceStateEx**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetdeviceinterfacestateex) 以启用此类接口。 

如果需要，驱动程序可以禁用并重新启用设备接口。 例如，如果驱动程序确定其设备已停止响应，则驱动程序可以调用 [**WdfDeviceSetDeviceInterfaceState**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetdeviceinterfacestate) 或 [**WdfDeviceSetDeviceInterfaceStateEx**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicesetdeviceinterfacestateex) 来禁用设备的接口，并禁止应用程序获取接口的新句柄。  (接口的现有句柄不受影响。 ) 如果该设备稍后变为可用，则驱动程序可以再次调用 **WdfDeviceSetDeviceInterfaceState** 或 **WdfDeviceSetDeviceInterfaceStateEx** 来重新启用接口。

### <a name="receiving-requests-to-access-a-device-interface"></a>接收访问设备接口的请求

当应用程序或内核模式组件请求访问驱动程序的设备接口时，框架会调用驱动程序的 [*EvtDeviceFileCreate*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_file_create) 回调函数。 驱动程序可以调用 [**WdfFileObjectGetFileName**](/windows-hardware/drivers/ddi/wdffileobject/nf-wdffileobject-wdffileobjectgetfilename) 来获取应用程序或内核模式组件正在访问的设备或文件的名称。 如果驱动程序在注册设备接口时指定了引用字符串，则操作系统会在 **WdfFileObjectGetFileName** 返回的文件或设备名称中包含引用字符串。

### <a name="accessing-another-drivers-device-interface"></a>访问另一个驱动程序的设备接口

本部分说明 Kernel-Mode Driver Framework 如何 (KMDF) 驱动程序或 User-Mode 驱动程序框架 (UMDF) 版本2驱动程序注册接收或删除其他驱动程序提供的设备接口的通知，然后创建 [远程 i/o 目标](general-i-o-targets-in-umdf.md) 以与设备接口所表示的设备通信。

有关如何在 UMDF 版本1驱动程序中执行此操作的信息，请参阅在 [Umdf 驱动程序中使用设备接口](using-device-interfaces-in-umdf-drivers.md#accessing-another-drivers-device-interface)。

若要注册设备接口事件的通知，KMDF 驱动程序将调用 [**IoRegisterPlugPlayNotification**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterplugplaynotification)，而 UMDF 2 驱动程序将调用 [**CM \_ 注册 \_ 通知**](/windows/win32/api/cfgmgr32/nf-cfgmgr32-cm_register_notification)。 在这两种情况下，驱动程序从其 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add) 回调函数调用适当的例程。

下面的代码示例演示本地 UMDF 2 驱动程序如何为通知注册，然后打开远程 i/o 目标。

1.  远程驱动程序通过从 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)调用 [**WdfDeviceCreateDeviceInterface**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreatedeviceinterface)来注册设备接口。
    ```cpp
        UNICODE_STRING ref;
        RtlInitUnicodeString(&ref, MY_HID_FILTER_REFERENCE_STRING);
        status = WdfDeviceCreateDeviceInterface(
                     hDevice,
                     (LPGUID) &GUID_DEVINTERFACE_MY_HIDFILTER_DRIVER,
                     &ref // ReferenceString
                 );

        if (!NT_SUCCESS (status)) {
            MyKdPrint( ("WdfDeviceCreateDeviceInterface failed 0x%x\n", status));
            return status;
        }

    ```

2.  本地驱动程序从 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)调用 [**CM \_ 注册 \_ 通知**](/windows/win32/api/cfgmgr32/nf-cfgmgr32-cm_register_notification)，以便在设备接口可用时注册通知。 提供一个指针，该指针指向框架在设备接口可用时调用的通知回调例程。
    ```cpp
    DWORD cmRet;
        CM_NOTIFY_FILTER cmFilter;

        ZeroMemory(&cmFilter, sizeof(cmFilter));
        cmFilter.cbSize = sizeof(cmFilter);
        cmFilter.FilterType = CM_NOTIFY_FILTER_TYPE_DEVICEINTERFACE;
        cmFilter.u.DeviceInterface.ClassGuid = GUID_DEVINTERFACE_MY_HIDFILTER_DRIVER;

        cmRet = CM_Register_Notification(
                    &cmFilter,                     // PCM_NOTIFY_FILTER pFilter,
                    (PVOID) hDevice,               // PVOID pContext,
                    MyCmInterfaceNotification,    // PCM_NOTIFY_CALLBACK pCallback,
                    &fdoData->CmNotificationHandle // PHCMNOTIFICATION pNotifyContext
                    );
        if (cmRet != CR_SUCCESS) {
            MyKdPrint( ("CM_Register_Notification failed, error %d\n", cmRet));
            status = STATUS_UNSUCCESSFUL;
            return status;
        }   
    ```

3.  每次指定的设备接口到达或删除时，系统都会调用本地驱动程序的通知回调例程。 回调例程可以检查 *EventData* 参数，以确定已到达的设备接口。 然后，它可能将工作项排队以打开设备接口。
    ```cpp
    DWORD 
    MyCmInterfaceNotification(
        _In_ HCMNOTIFICATION       hNotify,
        _In_opt_ PVOID             Context,
        _In_ CM_NOTIFY_ACTION      Action,
        _In_reads_bytes_(EventDataSize) PCM_NOTIFY_EVENT_DATA EventData,
        _In_ DWORD                 EventDataSize
        )
    {
        PFDO_DATA fdoData;
        UNICODE_STRING name;
        WDFDEVICE device;
        NTSTATUS status;
        WDFWORKITEM workitem;

        UNREFERENCED_PARAMETER(hNotify);
        UNREFERENCED_PARAMETER(EventDataSize);

        device = (WDFDEVICE) Context;
        fdoData = ToasterFdoGetData(device);

        switch(Action) {
        case CM_NOTIFY_ACTION_DEVICEINTERFACEARRIVAL: 
            MyKdPrint( ("MyCmInterfaceNotification: Arrival of %S\n",
                EventData->u.DeviceInterface.SymbolicLink));

            //
            // Enqueue a work item to open target
            //

            break;
        case CM_NOTIFY_ACTION_DEVICEINTERFACEREMOVAL: 
            MyKdPrint( ("MyCmInterfaceNotification: removal of %S\n",
                EventData->u.DeviceInterface.SymbolicLink));
            break;
        default:
            MyKdPrint( ("MyCmInterfaceNotification: Arrival unknown action\n"));
            break;
        }

        return 0;
    }
    ```


4.  从工作项回调函数中，本地驱动程序调用 [**WdfIoTargetCreate**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetcreate) 创建远程目标，并使用 [**WdfIoTargetOpen**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetopen) 打开远程 i/o 目标。

    调用 [**WdfIoTargetOpen**](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetopen)时，驱动程序可以选择注册 [*EvtIoTargetQueryRemove*](/windows-hardware/drivers/ddi/wdfiotarget/nc-wdfiotarget-evt_wdf_io_target_query_remove) 回调函数以接收删除通知，以及拒绝删除。 如果驱动程序未提供 *EvtIoTargetQueryRemove*，则在删除设备时，框架会关闭 i/o 目标。

    在极少数情况下，UMDF 2 驱动程序可以第二次调用 [**CM \_ 注册 \_ 通知**](/windows/win32/api/cfgmgr32/nf-cfgmgr32-cm_register_notification) ，以注册设备删除的通知。 例如，如果驱动程序调用 [**CreateFile**](/windows/win32/api/fileapi/nf-fileapi-createfilea) 来获取设备接口的句柄，则它应注册设备删除的通知，以便它能够正确响应查询删除尝试。 在大多数情况下，UMDF 2 驱动程序只调用 **CM \_ 注册 \_ 通知** 一次，并依赖于 WDF 对设备删除的支持。

    ```cpp
    VOID 
    EvtWorkItem(
        _In_ WDFWORKITEM WorkItem
    )
    {
        // 
        // create and open remote target
        //

        return;
    }
    ```

## <a name="related-topics"></a>相关主题

[注册获取设备接口到达和设备删除通知](../install/registering-for-notification-of-device-interface-arrival-and-device-removal.md)
