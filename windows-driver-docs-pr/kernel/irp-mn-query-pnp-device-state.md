---
title: IRP_MN_QUERY_PNP_DEVICE_STATE
description: 函数、筛选器和总线驱动程序可处理此请求。
ms.date: 08/12/2017
keywords:
- IRP_MN_QUERY_PNP_DEVICE_STATE Kernel-Mode 驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: fe45dcc9aa36d32ef7561ea6b0d4849a6a923214
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836917"
---
# <a name="irp_mn_query_pnp_device_state"></a>IRP \_ MN \_ 查询 \_ PNP \_ 设备 \_ 状态


函数、筛选器和总线驱动程序可处理此请求。

## <a name="value47"></a>Value47

0x14

<a name="major-code"></a>主要代码
----------

[**IRP \_ MJ \_ PNP**](irp-mj-pnp.md)

<a name="when-sent"></a>发送时间
---------

设备的驱动程序在设备首次启动时发送的 [**irp \_ MN \_ START \_ 设备**](irp-mn-start-device.md) 请求成功返回后，PnP 管理器会发送此 IRP。 停止资源重新平衡后，不会在开始时发送此 IRP。 当设备的驱动程序调用 [**IoInvalidateDeviceState**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinvalidatedevicestate)时，PnP 管理器还会发送此 IRP。

PnP 管理器在任意线程的上下文中以 IRQL 被动级别发送此 IRP \_ 。

## <a name="input-parameters"></a>输入参数


无

## <a name="output-parameters"></a>输出参数


在 i/o 状态块中返回。

## <a name="io-status-block"></a>I/o 状态块


驱动程序将 **Irp- &gt; IoStatus** 设置为状态 " \_ 成功"，或设置为适当的错误状态，如状态 "未 \_ 成功"。

成功时，驱动程序将 **Irp- &gt; IoStatus** 设置为 [**PNP \_ 设备 \_ 状态**](./handling-an-irp-mn-surprise-removal-request.md#about-pnp_device_state) 位掩码。


如果函数或筛选器驱动程序不处理此 IRP，它将调用 [**IoSkipCurrentIrpStackLocation**](./mm-bad-pointer.md)，不会设置 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程，并将 IRP 向下传递到下一个驱动程序。 此类驱动程序不得修改 **irp- &gt; IoStatus** 并且不得完成 irp。

如果总线驱动程序未处理此 IRP，它会将 **irp- &gt; IoStatus** 保持原样，并完成 irp。

<a name="operation"></a>操作
---------

此 IRP 首先由设备堆栈顶部的驱动程序和堆栈中的每个下一个较低的驱动程序处理。

如果驱动程序包含有关设备 PnP 状态的信息，则该驱动程序将处理此 IRP。 驱动程序可以在 PNP \_ 设备状态位掩码中设置或清除标志 \_ 。 如果其他驱动程序已 \_ \_ 在 **Irp- &gt; IoStatus** 中设置 PNP 设备状态，则驱动程序必须小心修改该位掩码中的标志，而不是覆盖整个结构。

请参阅 [即插即用](./introduction-to-plug-and-play.md) ，了解用于处理 [即插即用次要 irp](plug-and-play-minor-irps.md)的一般规则。

**正在发送此 IRP**

预留给系统使用。 驱动程序不得发送此 IRP。

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


[**IoInvalidateDeviceState**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinvalidatedevicestate)

[**PNP \_ 设备 \_ 状态**](./handling-an-irp-mn-surprise-removal-request.md#about-pnp_device_state)
