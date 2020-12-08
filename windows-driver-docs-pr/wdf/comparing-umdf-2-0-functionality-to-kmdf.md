---
title: 将 UMDF 2 功能与 KMDF 进行比较
description: 本主题将 Kernel-Mode Driver Framework 可用的功能与 (KMDF) 驱动程序的功能进行比较，该驱动程序可用于 User-Mode Driver Framework (UMDF) 2 驱动程序。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 73e07c67b84f483684c119f0a07175bb228404a7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837049"
---
# <a name="comparing-umdf-2-functionality-to-kmdf"></a>将 UMDF 2 功能与 KMDF 进行比较


本主题将 Kernel-Mode Driver Framework 可用的功能与 (KMDF) 驱动程序的功能进行比较，该驱动程序可用于 User-Mode Driver Framework (UMDF) 2 驱动程序。 它旨在帮助您决定是否应该编写 UMDF 2 驱动程序或 KMDF 驱动程序。

虽然 UMDF 版本2提供了一项非常重要的功能，这些功能以前仅适用于 KMDF 驱动程序，但以下功能仅适用于 KMDF 驱动程序。 如果驱动程序需要这些功能之一，则必须编写 KMDF 驱动程序。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">功能</th>
<th align="left">相关信息</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"> (DMA) 的直接内存访问</td>
<td align="left"><a href="/windows-hardware/drivers/wdf/introduction-to-dma-in-windows-driver-framework">在 KMDF 驱动程序中处理 DMA 操作</a></td>
</tr>
<tr class="even">
<td align="left">总线枚举</td>
<td align="left"><a href="enumerating-the-devices-on-a-bus.md" data-raw-source="[Enumerating the Devices on a Bus](enumerating-the-devices-on-a-bus.md)">枚举总线上的设备</a></td>
</tr>
<tr class="odd">
<td align="left">UMDF) 提供功能电源状态 (有限支持</td>
<td align="left"><a href="supporting-functional-power-states.md" data-raw-source="[Supporting Functional Power States](supporting-functional-power-states.md)">支持功能性电源状态</a></td>
</tr>
<tr class="even">
<td align="left">访问 WDM 对象和 Irp</td>
<td align="left"><a href="obtaining-wdm-information.md" data-raw-source="[Obtaining WDM Information](obtaining-wdm-information.md)">获取 WDM 信息</a></td>
</tr>
<tr class="odd">
<td align="left">未缓冲或直接 i/o</td>
<td align="left"><p><a href="accessing-data-buffers-in-wdf-drivers.md#neither" data-raw-source="[Accessing Data Buffers in WDF Drivers](accessing-data-buffers-in-wdf-drivers.md#neither)">访问 WDF 驱动程序中的数据缓冲区</a></p>
<p><a href="managing-i-o-queues.md#obtaining-requests-from-an-i-o-queue" data-raw-source="[Intercepting an I/O Request before it is Queued](managing-i-o-queues.md#obtaining-requests-from-an-i-o-queue)">正在截获 i/o 请求，并将其排入队列</a></p>
<ul>
<li><a href="/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_io_in_caller_context" data-raw-source="[&lt;em&gt;EvtIoInCallerContext&lt;/em&gt;](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_io_in_caller_context)"><em>EvtIoInCallerContext</em></a></li>
</ul></td>
</tr>
<tr class="even">
<td align="left">内部设备控制请求 (IOCTLs) </td>
<td align="left"><p><a href="sending-i-o-requests-synchronously.md" data-raw-source="[Sending I/O Requests Synchronously](sending-i-o-requests-synchronously.md)">同步发送 I/O 请求</a></p>
<ul>
<li><a href="/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendinternalioctlsynchronously" data-raw-source="[&lt;strong&gt;WdfIoTargetSendInternalIoctlSynchronously&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendinternalioctlsynchronously)"><strong>WdfIoTargetSendInternalIoctlSynchronously</strong></a></li>
<li><a href="/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendinternalioctlotherssynchronously" data-raw-source="[&lt;strong&gt;WdfIoTargetSendInternalIoctlOthersSynchronously&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetsendinternalioctlotherssynchronously)"><strong>WdfIoTargetSendInternalIoctlOthersSynchronously</strong></a></li>
</ul>
<p><a href="sending-i-o-requests-asynchronously.md" data-raw-source="[Sending I/O Requests Asynchronously](sending-i-o-requests-asynchronously.md)">异步发送 I/O 请求</a></p>
<ul>
<li><a href="/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforinternalioctl" data-raw-source="[&lt;strong&gt;WdfIoTargetFormatRequestForInternalIoctl&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforinternalioctl)"><strong>WdfIoTargetFormatRequestForInternalIoctl</strong></a></li>
<li><a href="/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforinternalioctlothers" data-raw-source="[&lt;strong&gt;WdfIoTargetFormatRequestForInternalIoctlOthers&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfiotarget/nf-wdfiotarget-wdfiotargetformatrequestforinternalioctlothers)"><strong>WdfIoTargetFormatRequestForInternalIoctlOthers</strong></a></li>
</ul></td>
</tr>
<tr class="odd">
<td align="left">取消选择对 i/o 请求的锁定</td>
<td align="left"><a href="/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetremovelockoptions" data-raw-source="[&lt;strong&gt;WdfDeviceInitSetRemoveLockOptions&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfdevice/nf-wdfdevice-wdfdeviceinitsetremovelockoptions)"><strong>WdfDeviceInitSetRemoveLockOptions</strong></a></td>
</tr>
<tr class="even">
<td align="left">WMI</td>
<td align="left"><a href="introduction-to-wmi-for-kmdf-drivers.md" data-raw-source="[Introduction to WMI for KMDF Drivers](introduction-to-wmi-for-kmdf-drivers.md)">用于 KMDF 驱动程序的 WMI 简介</a></td>
</tr>
</tbody>
</table>

 

如果你的驱动程序没有上述任何要求，则可以编写一个 UMDF 2 驱动程序，而不是使用 KMDF。 由于这两个框架共享多个接口，因此，如果需要，可以稍后将驱动程序转换为 KMDF。 有关为何要选择 UMDF 的详细信息，请参阅 [编写 Umdf 驱动程序的优点](advantages-of-writing-umdf-drivers.md)。

有关 KMDF 和 UMDF 支持的框架对象和的详细信息，请参阅 [框架对象的摘要](summary-of-framework-objects.md)。

有关显示所有 Windows 驱动程序框架 (WDF) 回调和方法及其框架适用性的表，请参阅 [Wdf 回调和方法摘要](/windows-hardware/drivers/ddi/_wdf/)。

