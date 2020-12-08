---
title: 'IoBuildDeviceIoControlSetEvent 规则 (wdm) '
description: IoBuildDeviceIoControlSetEvent 规则指定如果驱动程序提供指向调用方分配和初始化的事件对象的指针，则调用 IoBuildDeviceIoControlRequest 的驱动程序不得调用 KeSetEvent。
ms.date: 05/21/2018
keywords:
- 'IoBuildDeviceIoControlSetEvent 规则 (wdm) '
topic_type:
- apiref
api_name:
- IoBuildDeviceIoControlSetEvent
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 39f462d2dc3bda7d61e5aeff21a5c2ef996abc80
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839657"
---
# <a name="iobuilddeviceiocontrolsetevent-rule-wdm"></a>IoBuildDeviceIoControlSetEvent 规则 (wdm) 


**IoBuildDeviceIoControlSetEvent** 规则指定如果驱动程序提供指向调用方分配和初始化的事件对象的指针，则调用 [**IoBuildDeviceIoControlRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest)的驱动程序不得调用 [**KeSetEvent**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent) 。 此 IRP 的驱动程序无需调用 **KeSetEvent** 。

**驱动程序模型： WDM**

<a name="how-to-test"></a>如何测试
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在编译时</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>IoBuildDeviceIoControlSetEvent</strong> 规则。</p>
使用以下步骤来运行代码分析：
<ol>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](./using-static-driver-verifier-to-find-defects-in-drivers.md#preparing-your-source-code)">准备你的代码 (使用) 的角色类型声明。</a></li>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](./using-static-driver-verifier-to-find-defects-in-drivers.md#running-static-driver-verifier)">运行静态驱动程序验证程序。</a></li>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](./using-static-driver-verifier-to-find-defects-in-drivers.md#viewing-and-analyzing-the-results)">查看并分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅 <a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](./using-static-driver-verifier-to-find-defects-in-drivers.md)">使用静态驱动程序验证器查找驱动程序中的缺陷</a>。</p></td>
</tr>
</tbody>
</table>

<a name="applies-to"></a>适用于
----------

[**IoBuildDeviceIoControlRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iobuilddeviceiocontrolrequest) 
[**KeClearEvent**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keclearevent) 
[**KeInitializeEvent**](/windows-hardware/drivers/ddi/wdm/nf-wdm-keinitializeevent) 
[**KeSetEvent**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kesetevent)
