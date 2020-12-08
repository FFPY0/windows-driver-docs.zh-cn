---
title: 框架对象
description: 框架对象
keywords:
- UMDF 对象 WDK，已列出
- framework 对象 WDK UMDF，已列出
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 05a53f333825d6a0b008fe5d5bfff39fdbcef904
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96815671"
---
# <a name="framework-objects"></a>框架对象


[!include[UMDF 1 Deprecation](../includes/umdf-1-deprecation.md)]

下表提供了有关每个框架对象的基本信息，链接到对象的接口，并链接到有关核心框架对象的详细信息。

<table style="width:100%;">
<colgroup>
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
<col width="16%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Objectname</th>
<th align="left">ObjectInterface</th>
<th align="left">目的</th>
<th align="left">Defaultparent</th>
<th align="left">驱动程序是否可以 overridedefaultparent？</th>
<th align="left">驱动程序是否可以拥有？</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="framework-driver-object.md" data-raw-source="[Driver object](framework-driver-object.md)">驱动程序对象</a></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdriver" data-raw-source="[IWDFDriver](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdriver)">IWDFDriver</a></p></td>
<td align="left"><p>表示驱动程序</p></td>
<td align="left"><p>无</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="framework-device-object.md" data-raw-source="[Device object](framework-device-object.md)">设备对象</a></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdevice" data-raw-source="[IWDFDevice](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfdevice)">IWDFDevice</a></p></td>
<td align="left"><p>表示设备</p></td>
<td align="left"><p>驱动程序对象</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>否</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="framework-file-object.md" data-raw-source="[File object](framework-file-object.md)">File 对象</a></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdffile" data-raw-source="[IWDFFile](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdffile)">IWDFFile</a></p></td>
<td align="left"><p>表示文件</p></td>
<td align="left"><p>设备对象</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p></p>
不，如果是由框架创建的;是（如果由驱动程序创建）</td>
</tr>
<tr class="even">
<td align="left"><p><a href="framework-interrupt-object.md" data-raw-source="[Interrupt object](framework-interrupt-object.md)">中断对象</a></p></td>
<td align="left"><a href="/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfinterrupt" data-raw-source="[IWDFInterrupt](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfinterrupt)">IWDFInterrupt</a></td>
<td align="left"><p>表示中断</p></td>
<td align="left"><p>设备对象</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>是</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="framework-i-o-queue-object.md" data-raw-source="[Queue object](framework-i-o-queue-object.md)">Queue 对象</a></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfioqueue" data-raw-source="[IWDFIoQueue](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfioqueue)">IWDFIoQueue</a></p></td>
<td align="left"><p>表示接收 i/o 请求的 i/o 队列</p></td>
<td align="left"><p>设备对象</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>是</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="framework-i-o-request-object.md" data-raw-source="[Request object](framework-i-o-request-object.md)">请求对象</a></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiorequest" data-raw-source="[IWDFIoRequest](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiorequest)">IWDFIoRequest</a></p></td>
<td align="left"><p>表示 i/o 请求</p></td>
<td align="left"><p>设备对象</p></td>
<td align="left"><p></p>
不，如果是由框架创建的;是（如果由驱动程序创建）</td>
<td align="left"><p></p>
不，如果是由框架创建的 (例如，重定向的请求) ;是（如果由驱动程序创建）</td>
</tr>
<tr class="odd">
<td align="left"><p><a href="framework-i-o-target-object.md" data-raw-source="[Target object](framework-i-o-target-object.md)">目标对象</a></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiotarget" data-raw-source="[IWDFIoTarget](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfiotarget)">IWDFIoTarget</a></p></td>
<td align="left"><p>表示其他驱动程序将请求发送到的驱动程序</p></td>
<td align="left"><p>设备对象</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p></p>
"否" （对于默认目标）;是，适用于所有其他目标</td>
</tr>
<tr class="even">
<td align="left"><p>USB 设备对象</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetdevice" data-raw-source="[IWDFUsbTargetDevice](/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetdevice)">IWDFUsbTargetDevice</a></p></td>
<td align="left"><p>表示连接到 USB 的设备</p></td>
<td align="left"><p>设备对象</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>是 (请参阅目标对象) </p></td>
</tr>
<tr class="odd">
<td align="left"><p>USB 管道对象</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetpipe" data-raw-source="[IWDFUsbTargetPipe](/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbtargetpipe)">IWDFUsbTargetPipe</a></p></td>
<td align="left"><p>表示 USB 设备管道</p></td>
<td align="left"><p>设备对象</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>是 (请参阅目标对象) </p></td>
</tr>
<tr class="even">
<td align="left"><p>USB 接口对象</p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbinterface" data-raw-source="[IWDFUsbInterface](/windows-hardware/drivers/ddi/wudfusb/nn-wudfusb-iwdfusbinterface)">IWDFUsbInterface</a></p></td>
<td align="left"><p>表示 USB 设备接口</p></td>
<td align="left"><p>设备对象</p></td>
<td align="left"><p>否</p></td>
<td align="left"><p>是 (请参阅目标对象) </p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="framework-base-object.md" data-raw-source="[Base object](framework-base-object.md)">基对象</a></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfobject" data-raw-source="[IWDFObject](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfobject)">IWDFObject</a></p></td>
<td align="left"><p>表示常规基对象</p></td>
<td align="left"><p>驱动程序对象</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p>是（如果由驱动程序创建）</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="framework-memory-object.md" data-raw-source="[Memory object](framework-memory-object.md)">内存对象</a></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfmemory" data-raw-source="[IWDFMemory](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdfmemory)">IWDFMemory</a></p></td>
<td align="left"><p>表示内存对象</p></td>
<td align="left"><p>驱动程序对象</p></td>
<td align="left"><p>是</p></td>
<td align="left"><p></p>
不，如果是由框架创建的;是（如果由驱动程序创建）</td>
</tr>
</tbody>
</table>

 

