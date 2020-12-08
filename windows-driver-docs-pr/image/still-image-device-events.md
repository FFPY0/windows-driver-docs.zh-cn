---
title: 静态图像设备事件
description: 静态图像设备事件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d2dc0e726ea8015b42906e64f038ded3a85723a1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792865"
---
# <a name="still-image-device-events"></a>静态图像设备事件





" *静止图像设备事件* " 是指应向顶级软件通知上层软件的设备级别，前提是该软件已请求此类通知。 用户模式微型驱动程序负责定义大多数设备事件，并在事件发生时传递通知。 通常情况下，事件指示需要执行某个操作的高级软件。

典型的静止图像设备事件是检测到按下了 "推送" 按钮。 例如，扫描仪可能会为用户提供单独的按钮来启动扫描文本和照片。 按下按钮时，需要使用上层软件来显示或存储映像。 静态图像事件监视器检测到事件已 (使用 [ISTIDEVICE com 接口](istidevice-com-interface.md)) ，并且可以调用以前使用 [IStillImage COM 接口](istillimage-com-interface.md)) 注册 (的静止图像应用程序。

静止图像设备事件由 Guid 表示。 在 *sti* 中，Microsoft 定义了以下静止图像设备事件：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>事件 GUID</th>
<th>目的</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>GUID_DeviceArrivedLaunch</strong></p></td>
<td><p>静止图像设备刚刚附加到系统。</p></td>
</tr>
<tr class="even">
<td><p><strong>GUID_ScanImage</strong></p></td>
<td><p>应将图像扫描到计算机中。</p></td>
</tr>
<tr class="odd">
<td><p><strong>GUID_ScanFaxImage</strong></p></td>
<td><p>应将图像扫描到计算机，然后再将其传真。</p></td>
</tr>
<tr class="even">
<td><p><strong>GUID_ScanPrintImage</strong></p></td>
<td><p>应将图像扫描到计算机，然后再进行打印。</p></td>
</tr>
<tr class="odd">
<td><p><strong>GUID_STIUserDefined1</strong></p></td>
<td><p>已按用户可定义的按钮。</p></td>
</tr>
<tr class="even">
<td><p><strong>GUID_STIUserDefined2</strong></p></td>
<td><p>已按用户可定义的按钮。</p></td>
</tr>
<tr class="odd">
<td><p><strong>GUID_STIUserDefined3</strong></p></td>
<td><p>已按用户可定义的按钮。</p></td>
</tr>
</tbody>
</table>

 

用户模式微型驱动程序的开发人员应尽可能使用这些预定义的事件 Guid。 如果这些 Guid 不合适，则必须定义特定于设备的事件的 Guid。

若要定义静止图像设备事件，必须执行以下操作：

-   为每个事件指定一个 GUID。

-   在用户模式驱动程序的 INF 文件中包括每个 GUID。

在驱动程序的 INF 文件中，每个 GUID 规范都必须包含一个星号 (表示 "所有应用程序" ) 或特定应用程序的列表，指示事件发生时应启动的应用程序。 静止图像事件监视器使用此列表向事件提供应用程序的默认分配。 用户可以通过 "扫描仪和照相机" 控制面板修改这些分配。

### <a name="event-notification"></a>事件通知

驱动程序必须使用异步 i/o 或轮询) 来监视设备 (，以确定与每个 GUID 关联的事件发生的时间。 根据设备功能，驱动程序可能会以异步方式或通过响应轮询设备的请求通知客户端出现的设备事件。 所有能够提供) 任一方法都 (设备事件通知的驱动程序必须 \_ \_ 在设备的 [**STI \_ DEV \_ cap**](/windows-hardware/drivers/ddi/sti/ns-sti-_sti_dev_caps) 结构中设置 STI GENCAP 通知标志。 支持轮询的驱动程序，而不是异步通知，还必须 \_ \_ 在相同的结构中设置 STI GENCAP 轮询 \_ 必需标志。 此外，还必须使用 INF 文件中的 " **功能** " 关键字 [为静止图像设备](inf-files-for-still-image-devices.md)指定这些功能 (。 ) 

如果驱动程序支持事件的异步通知，则事件监视器将调用 [**IStiUSD：： SetNotificationHandle**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-setnotificationhandle) 来请求通知并提供事件句柄。 发生设备事件时，驱动程序必须通过调用 **SetEvent** 通知事件监视器 (参阅 Microsoft Windows SDK 文档) ，使用事件句柄作为参数。 然后，客户端可以调用 [**IStiUSD：： GetNotificationData**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getnotificationdata) 以获取事件的 GUID。

如果需要轮询，事件监视器将调用 [**IStiUSD：： GetStatus**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getstatus) 来轮询驱动程序，该驱动程序必须依次轮询设备并返回 [**STI \_ 设备 \_ 状态**](/windows-hardware/drivers/ddi/sti/ns-sti-_sti_device_status) 结构中的结果。

 

