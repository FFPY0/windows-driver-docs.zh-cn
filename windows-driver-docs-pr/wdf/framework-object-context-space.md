---
title: 框架对象上下文空间
description: 框架对象上下文空间
keywords:
- framework 对象 WDK KMDF，上下文空间
- 上下文空间 WDK KMDF
- 对象上下文空间 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 492402227f4dbf44e340708701010ebc5ddedd9a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814789"
---
# <a name="framework-object-context-space"></a>框架对象上下文空间





*对象上下文空间* 是驱动程序可以分配并分配给对象的额外的不可分页内存空间。 每个基于框架的驱动程序可以为驱动程序接收或创建的每个框架对象创建一个或多个特定于对象的上下文空间。

基于框架的驱动程序应在数据所属对象的上下文空间内按值或指针存储所有对象特定数据。

例如，USB 设备的驱动程序可能会为其框架设备对象创建上下文空间。 在上下文空间中，驱动程序可能将此类特定于设备的信息存储为设备的 [**usb \_ 设备 \_ 描述符**](/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_device_descriptor) 和 [**USB \_ 配置 \_ 描述符**](/windows-hardware/drivers/ddi/usbspec/ns-usbspec-_usb_configuration_descriptor) 结构，以及表示设备接口管道的 [集合对象](framework-object-collections.md) 的句柄。

框架不会将框架对象从一个驱动程序传递到另一个驱动程序，因此不能使用对象的上下文空间在两个驱动程序之间传递数据。

若要定义对象的上下文空间，必须创建一个或多个结构。 每个结构都表示一个单独的上下文空间。 驱动程序将使用每个结构成员来存储特定于对象的信息。 此外，您的驱动程序必须要求框架为每个结构生成一个 *访问器方法* 。 此访问器方法接受对象句柄作为输入，并返回对象的上下文空间的地址。

每当驱动程序调用对象创建方法（如 [**WdfDeviceCreate**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)）时，该方法都可以选择分配上下文空间。 所有对象创建方法都接受一个可选的 [**WDF \_ 对象 \_ 属性**](/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes) 结构作为输入。 此结构描述你希望框架为对象分配的上下文空间。

若要在驱动程序调用对象的创建方法之后向对象添加其他上下文空间，驱动程序可以调用 [**WdfObjectAllocateContext**](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectallocatecontext) 方法，如对象创建方法，接受 [**WDF \_ 对象 \_ 属性**](/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes) 结构作为输入。

当框架为对象分配上下文空间时，它也会将上下文空间初始化为零。

当框架或驱动程序删除框架对象时，框架会删除该对象的所有上下文空间。

如果驱动程序使用上下文空间来存储驱动程序在创建对象时所分配的缓冲区的指针，则驱动程序应提供 [*EvtCleanupCallback*](/windows-hardware/drivers/ddi/wdfobject/nc-wdfobject-evt_wdf_object_context_cleanup) 函数，该函数在删除对象时释放缓冲区。

若要为驱动程序创建的对象定义对象的上下文空间结构和访问器方法，您的驱动程序必须使用以下步骤：

1.  定义描述要存储的数据的结构。 例如，如果想要为驱动程序的设备对象创建上下文数据，则驱动程序可能会定义一个名为 "我的设备上下文" 的结构 \_ \_ 。

2.  使用 [**wdf \_ declare \_ 上下文 \_ 类型**](./wdf-declare-context-type.md) 宏或 [**\_ \_ \_ \_ 具有 \_ NAME 宏的 wdf 声明上下文类型**](./wdf-declare-context-type-with-name.md) 。 这两个宏均执行以下操作：

    -   创建和初始化 [**WDF \_ 对象 \_ 上下文 \_ 类型 \_ 信息**](/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_context_type_info) 结构。
    -   定义驱动程序稍后用于访问对象的上下文空间的访问器方法。 访问器方法的返回值是指向对象的上下文空间的指针。

    WDF \_ DECLARE \_ 上下文 \_ 类型宏根据您的结构名称创建访问器方法的名称。 例如，如果你的上下文结构的名称是 "我的 \_ 设备 \_ 上下文"，则宏会创建一个名为 **WdfObjectGet \_ MY \_ device \_ context** 的访问器方法。

    \_ \_ \_ 通过具有 NAME 宏的 WDF 声明上下文类型 \_ \_ ，您可以指定访问器方法的名称。 例如，可以指定 **GetMyDeviceContext** 作为设备对象的上下文访问器方法的名称。

3.  调用 [**WDF \_ 对象 \_ 属性 \_ INIT**](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdf_object_attributes_init) 初始化对象的 [**WDF \_ 对象 \_ 属性**](/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes) 结构。

4.  使用 [**wdf \_ 对象 \_ 特性 \_ set \_ 上下文 \_ 类型**](./wdf-object-attributes-set-context-type.md) 宏将 wdf 对象特性结构的 **ContextTypeInfo** 成员设置 \_ \_ 为 wdf \_ 对象 \_ 上下文 \_ 类型 \_ 信息结构的地址。

5.  调用对象创建方法，例如 [**WdfDeviceCreate**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)。

在您的驱动程序创建对象之后，驱动程序可以随时调用 [**WdfObjectAllocateContext**](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectallocatecontext) 来向对象添加额外的上下文空间。

由于步骤1和步骤2定义全局数据结构并创建驱动程序可调用的例程，因此您的驱动程序必须在声明全局数据的驱动程序区域中完成这些步骤，通常是标头文件。 不能从驱动程序的例程中完成这些步骤。

驱动程序必须在创建对象的驱动程序例程（如调用 [**WdfDeviceCreate**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdevicecreate)的 [*EvtDriverDeviceAdd*](/windows-hardware/drivers/ddi/wdfdriver/nc-wdfdriver-evt_wdf_driver_device_add)回调函数）内完成步骤3、4和5。

框架可以代表驱动程序创建两种类型的对象-框架请求对象和框架文件对象。 你的驱动程序可以通过分别调用 [**WdfDeviceInitSetRequestAttributes**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetrequestattributes) 和 [**WdfDeviceInitSetFileObjectConfig**](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetfileobjectconfig)来注册这些对象的上下文空间。 驱动程序还可以调用 [**WdfObjectAllocateContext**](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectallocatecontext) 来为这些对象分配上下文空间。

创建对象后，驱动程序可以使用以下任一方法获取指向对象上下文空间的指针：

-   通过使用 [**WDF \_ declare \_ 上下文 \_ 类型**](./wdf-declare-context-type.md) 或 [**\_ \_ \_ \_ 具有 \_ NAME 宏的 wdf declare 上下文类型**](./wdf-declare-context-type-with-name.md) ，调用你在前面过程中的步骤2中创建的上下文访问器方法。

-   调用 [**WdfObjectGetTypedContext**](./wdfobjectgettypedcontext.md)，提供驱动程序定义的上下文结构的名称。

如果你的驱动程序有上下文空间指针，则可以通过调用 [**WdfObjectContextGetObject**](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdfobjectcontextgetobject)找到上下文空间所属的对象。

 

