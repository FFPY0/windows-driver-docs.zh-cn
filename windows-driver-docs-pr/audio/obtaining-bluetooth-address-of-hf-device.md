---
title: 获取 HF 设备的蓝牙地址
description: "\"获取 HF 设备的蓝牙地址\" 主题演示了音频驱动程序如何获取配对的免提 (HF) 设备的蓝牙地址。"
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2241faf74969518564baefc0256a9dcf40309a35
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800975"
---
# <a name="obtaining-bluetooth-address-of-hf-device"></a>获取 HF 设备的蓝牙地址


"获取 HF 设备的蓝牙地址" 主题演示了音频驱动程序如何获取配对的免提 (HF) 设备的蓝牙地址。

地址字符串可用于唯一标识特定的成对 HF 设备。 例如，地址字符串可以用作传递给 IoRegisterDeviceInterface 的 *ReferenceString* 参数、传递给 KsCreateFilterFactory 的 *RefString* 参数或传递给 PcRegisterSubdevice 的 *Name* 参数。

请注意，GUID \_ DEVINTERFACE \_ BLUETOOTH \_ HFP \_ SCO \_ HCIBYPASS 设备接口符号链接对于每个配对 HF 设备也是唯一的，但对于某些用途，此字符串可能太长。

下面的代码示例中所示的 IoHelperGetDevicePdo 例程是 IoHelperGetDeviceBluetoothAddress 使用的实用函数。 在音频驱动程序处理 PnP 接口到达通知时，可以调用此类函数。 音频驱动程序从 Plxntb 获取设备对象并将其传递给 IoHelperGetDeviceBluetoothAddress。

```ManagedCPlusPlus
_IRQL_requires_(PASSIVE_LEVEL)
NTSTATUS
IoHelperGetDevicePdo(
    _In_ PDEVICE_OBJECT DeviceObject,
    _Out_ PDEVICE_OBJECT *PhysicalDeviceObject
    )

/*++

Routine description:
    Returns a pointer to the physical device object in a driver stack and
    increments the reference count on that object.

Parameters:
    DeviceObject
        Pointer to the device object for which the physical device object is
        retrieved. 

    PhysicalDeviceObject
        Returns a pointer to the physical device object in a stack of device
        objects after incrementing the reference count on the object.

Return value:
    A status code.

Remarks:
    This routine uses IRP_MN_QUERY_DEVICE_RELATIONS TargetDeviceRelation to
    get the physical device object from the device stack.

Requirements:
    IRQL    = PASSIVE_LEVEL

--*/

{
    NTSTATUS status;
    PIRP irp = NULL;
    PDEVICE_RELATIONS deviceRelations = NULL;
    PIO_STACK_LOCATION ioStack;
    KEVENT completionEvent;

    PAGED_CODE();

    irp = IoAllocateIrp(DeviceObject->StackSize, FALSE);
    if (irp == NULL)
    {
        status = STATUS_INSUFFICIENT_RESOURCES;
        goto Exit;
    }

    irp->IoStatus.Status = STATUS_NOT_SUPPORTED;

    ioStack = IoGetNextIrpStackLocation(irp);
    ioStack->MajorFunction = IRP_MJ_PNP;
    ioStack->MinorFunction = IRP_MN_QUERY_DEVICE_RELATIONS;
    ioStack->Parameters.QueryDeviceRelations.Type = TargetDeviceRelation;

    KeInitializeEvent(&completionEvent, SynchronizationEvent, FALSE);

    IoSetCompletionRoutine(irp, OnRequestComplete, &completionEvent, TRUE, TRUE, TRUE);

    status = IoCallDriver(DeviceObject, irp);
    if (status == STATUS_PENDING) {
        // wait for irp to complete
        KeWaitForSingleObject(
            &completionEvent,
            Suspended,
            KernelMode,
            FALSE,
            NULL);
        status = irp->IoStatus.Status;
    }

    if (NT_SUCCESS(status))
    {
        deviceRelations = (PDEVICE_RELATIONS)irp->IoStatus.Information;
        *PhysicalDeviceObject = deviceRelations->Objects[0];
    }

Exit:
    if (deviceRelations != NULL)
    {
        ExFreePool(deviceRelations);
    }
    if (irp != NULL)
    {
        IoFreeIrp(irp);
    }
    return status;
}

_IRQL_requires_(PASSIVE_LEVEL)
NTSTATUS IoHelperGetDeviceBluetoothAddress(
    _In_ PDEVICE_OBJECT DeviceObject,
    _Outptr_ PWSTR *BluetoothAddress,
    _In_ ULONG Tag
    )

/*++

Routine description:
    Returns the Bluetooth address string for the physical device object in the
    device stack.

Parameters:
    DeviceObject
        Pointer to a device object in a device stack whose physical object has
        a Bluetooth address property.

    BluetoothAddress
        Returns a string allocated from NonPagedPoolNx pool. 

    Tag

Return value:
    A status code.

Remarks:
    This routine retrieves the DEVPKEY_Bluetooth_DeviceAddress property from
    the physical device object in the device stack containing the specified
    device object.

Requirements:
    IRQL    = PASSIVE_LEVEL

--*/

{
    NTSTATUS status;
    PDEVICE_OBJECT physicalDeviceObject = NULL;
    PWSTR bluetoothAddress = NULL;
    ULONG requiredSize;
    DEVPROPTYPE devPropType;

    PAGED_CODE();

    status = IoHelperGetDevicePdo(DeviceObject, &physicalDeviceObject);
    if (!NT_SUCCESS(status))
    {
        goto Exit;
    }

    status = IoGetDevicePropertyData(physicalDeviceObject, &DEVPKEY_Bluetooth_DeviceAddress, LOCALE_NEUTRAL, 0, 0, NULL, &requiredSize, &devPropType);
    if (NT_SUCCESS(status) || devPropType != DEVPROP_TYPE_STRING)
    {
        status = STATUS_UNSUCCESSFUL;
        goto Exit;
    }
    if (status != STATUS_BUFFER_TOO_SMALL)
    {
        goto Exit;
    }

    bluetoothAddress = (PWCH)ExAllocatePoolWithTag(NonPagedPoolNx, requiredSize, Tag);
    if (bluetoothAddress == NULL)
    {
        status = STATUS_INSUFFICIENT_RESOURCES;
        goto Exit;
    }

    status = IoGetDevicePropertyData(physicalDeviceObject, &DEVPKEY_Bluetooth_DeviceAddress, LOCALE_NEUTRAL, 0, requiredSize, bluetoothAddress, &requiredSize, &devPropType);
    if (!NT_SUCCESS(status))
    {
        goto Exit;
    }

    *BluetoothAddress = bluetoothAddress;
    bluetoothAddress = NULL;
    status = STATUS_SUCCESS;

Exit:
    if (bluetoothAddress != NULL)
    {
        ExFreePoolWithTag(bluetoothAddress, Tag);
    }
    if (physicalDeviceObject != NULL)
    {
        ObDereferenceObject(physicalDeviceObject);
    }
    return status;
}
```

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题
[相关的设计指南](related-design-guidelines.md)  



