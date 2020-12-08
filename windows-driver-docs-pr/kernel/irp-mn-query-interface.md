---
title: IRP_MN_QUERY_INTERFACE
description: 通过 IRP_MN_QUERY_INTERFACE 请求，驱动程序可以将直接调用接口导出到其他驱动程序。导出接口的总线驱动程序必须 (子 PDOs) 为其子设备处理此请求。
ms.date: 08/12/2017
keywords:
- IRP_MN_QUERY_INTERFACE Kernel-Mode 驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 8a12f0939d57aefe9539d698307c09077ec6264a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816081"
---
# <a name="irp_mn_query_interface"></a>IRP \_ MN \_ 查询 \_ 接口


使用 **IRP \_ MN \_ QUERY \_ interface** request，驱动程序可以将直接调用接口导出到其他驱动程序。

导出接口的总线驱动程序必须 (子 PDOs) 为其子设备处理此请求。 函数和筛选器可以选择处理此请求。

此上下文中的 "接口" 由驱动程序或驱动程序集导出的一个或多个例程和可能的数据组成。 接口具有描述其内容的结构和标识其类型的 GUID。

例如，PCMCIA 总线驱动程序会导出 GUID \_ pcmcia \_ 接口标准类型的接口 \_ ，该接口包含用于操作的例程，如获取 PCMCIA 内存卡的写保护状态。 此类内存卡的函数驱动程序可以将 **IRP \_ MN \_ QUERY \_ INTERFACE** 请求发送到父 pcmcia 总线驱动程序，以获取指向 PCMCIA 接口例程的指针。

本部分介绍了查询界面 IRP 作为一般机制。 公开接口的驱动程序应提供有关其特定接口的其他信息。

## <a name="value"></a>“值”

0x08

<a name="major-code"></a>主要代码
----------

[**IRP \_ MJ \_ PNP**](irp-mj-pnp.md)

<a name="when-sent"></a>发送时间
---------

驱动程序或系统组件发送此 IRP，以获取有关设备驱动程序导出的接口的信息。

驱动程序或系统组件 \_ 在任意线程上下文中以 IRQL = 被动级别发送此 IRP。

在为设备调用了驱动程序的 [*AddDevice*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device) 例程之后，驱动程序可以随时接收此 IRP。 发送此 IRP 时，设备可能会也可能不会启动 (也就是说，您不能假定驱动程序已成功完成设备) 的 [**IRP \_ MN \_ 启动 \_ 设备**](irp-mn-start-device.md) 请求。

## <a name="input-parameters"></a>输入参数


[**IO \_ 堆栈 \_ 位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)结构的 **参数. QueryInterface** 成员本身是一个结构，它描述所请求的接口。 此结构包含以下信息：

```cpp
CONST GUID *InterfaceType;
USHORT Size;
USHORT Version;
PINTERFACE Interface;
PVOID InterfaceSpecificData
```

结构的成员定义如下：

<a href="" id="interfacetype"></a>**InterfaceType**  
指向标识所请求的接口的 GUID。 GUID 可以是系统定义的接口，如 GUID \_ 总线 \_ 接口 \_ 标准或自定义接口。 系统定义的接口的 Guid 列在 Wdmguid 中。 应通过 Uuidgen.exe 生成自定义接口的 Guid。

<a href="" id="size"></a>**规格**  
指定所请求的接口的大小。 处理此 IRP 的驱动程序不能返回大于 **大小** 字节的 [**接口**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_interface)结构。

<a href="" id="version"></a>**版本**  
指定所请求的接口的版本。

如果驱动程序支持多个版本的接口，则驱动程序将返回最近的受支持版本，而不会超出请求的版本。 发送 IRP 的组件应检查返回的 **接口. 版本** 字段，并根据该值确定要执行的操作。

<a href="" id="interface"></a>**交互**  
指向要返回所请求的接口的结构。 此结构必须包含 [**接口**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_interface) 结构作为其第一个成员。 发送 IRP 的组件会从分页内存中分配此结构。

导出接口的驱动程序会定义一个新的结构类型，该类型包含 **接口** 结构，以及接口中的例程和/或数据的成员。  (驱动程序还会定义接口的 GUID，如上面的 **InterfaceType** 成员中所述。 ) 

导出接口的驱动程序为接口中的每个例程定义执行环境，其中包括可以调用例程的 IRQL，等等。

<a href="" id="interfacespecificdata"></a>**InterfaceSpecificData**  
指定有关所请求的接口的其他信息。

对于某些接口，发送 IRP 的组件会在此字段中指定其他信息。 通常，此字段为 **NULL** ， **InterfaceType** 和 **Version** 足以标识所请求的接口。

## <a name="output-parameters"></a>输出参数


成功时，驱动程序将填充参数的成员 **。**

## <a name="io-status-block"></a>I/o 状态块


驱动程序将 **Irp- &gt; IoStatus** 设置为状态 " \_ 成功" 或相应的 "错误" 状态。

如果成功，则总线驱动程序将 **Irp- &gt; IoStatus** 设置为零。

如果函数或筛选器驱动程序不处理此 IRP，它将调用 [**IoSkipCurrentIrpStackLocation**](./mm-bad-pointer.md) 并将 IRP 向下传递到下一个驱动程序。 此类驱动程序不得修改 **&gt; IoStatus 状态** ，并且不能完成 irp。

如果总线驱动程序不会导出请求的接口，因此不会为子 PDO 处理此 IRP，则总线驱动程序会保留 **&gt; IoStatus** ，并完成 irp。

<a name="operation"></a>操作
---------

如果参数指定了驱动程序支持的接口，则驱动程序将处理此 IRP。

如果 IRP 请求驱动程序不支持的接口，则驱动程序不得将此 IRP 排队。 驱动程序必须检查其 [**IO \_ 堆栈 \_ 位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)结构中的 **InterfaceType** 。 如果接口不是驱动程序支持的接口，则驱动程序必须将 IRP 传递到设备堆栈中的下一个较低的驱动程序，而不会受到阻止。

每个接口都必须提供 **InterfaceReference** 和 **InterfaceDereference** 例程，并且导出接口的驱动程序必须在 [**接口**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_interface) 结构中提供这些例程的地址。 在驱动程序返回接口以响应 IRP 之前，它必须通过调用其 **InterfaceReference** 例程来递增接口的引用计数。 当请求接口的驱动程序使用完该驱动程序时，该驱动程序必须通过调用接口的 **InterfaceDereference** 例程来减小引用计数。

如果发送 IRP (driver *x*) 的驱动程序稍后会将该接口传递到另一个驱动程序 (驱动程序 *y*) 那么，驱动程序 *x* 必须递增该接口的引用计数，并且驱动程序 *y* 必须将其减小。

处理此 IRP 的驱动程序应避免将 IRP 传递到另一个设备堆栈以获取所请求的接口。 此类设计会在难以管理的设备堆栈之间创建依赖关系。 例如，在第一个堆栈中的相应驱动程序取消引用接口之前，不能删除第二个设备堆栈所表示的设备。

接口可以是特定于总线或与总线无关的。 特定于总线的接口是在这些总线的标头文件中定义的。 系统为导出标准总线接口定义与总线无关的接口（ [**总线 \_ 接口 \_ 标准**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_bus_interface_standard)）。

请参阅 [即插即用](./introduction-to-plug-and-play.md) ，了解用于处理 [即插即用次要 irp](plug-and-play-minor-irps.md)的一般规则。

此 IRP 专用于在设备的分层内核模式驱动程序之间传递例程入口点。 不要将此 IRP 公开的接口与 *设备接口* 混淆。 设备接口主要用于公开设备的路径，供用户模式组件或其他内核组件使用。 有关设备接口的详细信息，请参阅 [设备接口类](../install/overview-of-device-interface-classes.md)。

**正在发送此 IRP**

有关发送 Irp 的信息，请参阅 [处理 irp](./handling-irps.md) 。 以下步骤专门适用于此 IRP：

-   从分页池分配 [**接口**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_interface) 结构，并将其初始化为零。 如果 &gt; 根据接口协定，将在 IRQL = 调度 \_ 级别调用接口，则调用方可以将内容复制到从非分页池分配的内存。

-   在 IRP 的下一个 i/o 堆栈位置设置值：将 **MajorFunction** 设置为 [**irp \_ MJ \_ PNP**](irp-mj-pnp.md)，将 **MinorFunction** 设置为 **irp \_ MN \_ 查询 \_ 接口**，并在参数中设置相应的值 **。**

-   将 **IoStatus** 初始化为 \_ 不 \_ 受支持的状态。

-   当不再需要 IRP 和 **接口** 结构时，将其解除分配。

-   如接口的规范中所述，使用接口例程和上下文参数。

-   当不再需要接口时，使用 [*InterfaceDereference*](/windows-hardware/drivers/ddi/wdm/nc-wdm-pinterface_dereference) 例程递减引用计数。 取消引用接口后，不要调用任何接口例程。

驱动程序通常将此 IRP 发送到连接驱动程序的设备堆栈的顶部。 如果驱动程序将此 IRP 发送到不同的设备堆栈，则驱动程序必须在另一台设备上注册目标设备通知（如果其他设备不是驱动程序所服务的设备的祖先）。 此类驱动程序使用 **EventCategoryTargetDeviceChange** 的 *EventCategory* 调用 [**IoRegisterPlugPlayNotification**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterplugplaynotification) 。 当驱动程序接收到类型 GUID \_ 目标 \_ 设备查询删除的通知时 \_ \_ ，驱动程序必须取消对接口的引用。 如果接口收到后续的 GUID \_ 目标 \_ 设备 \_ 删除已取消的 \_ 通知，则该驱动程序可以重新查询该驱动程序。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Wdm.h（包括 Wdm.h、Ntddk.h 或 Ntifs.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**总线 \_ 接口 \_ 标准**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_bus_interface_standard)

[**交互**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_interface)

[**IoRegisterPlugPlayNotification**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioregisterplugplaynotification)

 

