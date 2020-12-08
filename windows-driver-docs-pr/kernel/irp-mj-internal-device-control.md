---
title: IRP_MJ_INTERNAL_DEVICE_CONTROL
description: 通常，任何支持内部设备控制请求的现有驱动程序的替换都应在 DispatchInternalDeviceControl 例程中处理此请求。
ms.date: 08/12/2017
keywords:
- IRP_MJ_INTERNAL_DEVICE_CONTROL Kernel-Mode 驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: bd98bb4cfdf2718d4c483569862ee6a4784bdfe8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822325"
---
# <a name="irp_mj_internal_device_control"></a>IRP\_MJ\_INTERNAL\_DEVICE\_CONTROL


通常，任何支持内部设备控制请求的现有驱动程序的替换都应在 [*DispatchInternalDeviceControl*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程中处理此请求。 此类驱动程序必须支持与它所替换的驱动程序相同的一组内部 i/o 控制代码。 否则，现有的高级驱动程序可能无法与新的驱动程序一起工作。

需要用来替换特定较低级别系统驱动程序的驱动程序来处理此请求。 例如，系统并行端口驱动程序的替代必须继续支持现有的并行类驱动程序。 请注意，不能替换处理此请求的某些系统驱动程序，特别是系统提供的 SCSI 和视频端口驱动程序。

<a name="when-sent"></a>发送时间
---------

Create 请求成功完成之后的任何时间。

## <a name="input-parameters"></a>输入参数


I/o 控制代码包含在 IRP 的 i/o 堆栈位置的 **DeviceIoControl. IoControlCode** 中。

其他输入参数取决于 i/o 控制代码的值。 有关详细信息，请参阅 [I/o 控制代码的缓冲区说明](./buffer-descriptions-for-i-o-control-codes.md)。

## <a name="output-parameters"></a>输出参数


输出参数取决于 i/o 控制代码的值。 有关详细信息，请参阅 [I/o 控制代码的缓冲区说明](./buffer-descriptions-for-i-o-control-codes.md)。

<a name="operation"></a>操作
---------

当另一个驱动程序调用 [**IoBuildDeviceIoControlRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)或 [**IoAllocateIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)来创建请求时，驱动程序将接收 **IRP \_ MJ \_ 内部 \_ 设备 \_ 控制** 请求。

已为成对的和分层的内核模式驱动程序（如通过端口驱动程序分层的一个或多个类驱动程序）之间的通信定义了此 i/o 控制代码。 较高级别的驱动程序通过设备或驱动程序特定的 i/o 控制代码设置 Irp，并从下一个较低版本的驱动程序请求支持。

请求的操作是特定于设备或驱动程序的。

有关 [**irp \_ mj \_ 设备 \_ 控制**](irp-mj-device-control.md) 或 **irp \_ mj \_ 内部 \_ 设备 \_ 控制** 请求的 I/o 控制代码的常规信息，请参阅 [使用 i/o 控制代码](./introduction-to-i-o-control-codes.md)。 另请参阅 [设备 Type-Specific I/o 请求](./device-type-specific-i-o-requests.md)。

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


[*DispatchInternalDeviceControl*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch)

[**IoAllocateIrp**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateirp)

[**IoBuildDeviceIoControlRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)

