---
title: 关于传感器参数类型
description: 关于参数类型
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: c7fa57caf884c1483f6fb8cf8d351fc95ebebe76
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831095"
---
# <a name="about-sensor-parameter-types"></a>关于传感器参数类型


你应了解传感器类扩展如何使用某些数据类型作为方法参数。 下表描述了这些数据类型。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>类型</th>
<th>参数名称</th>
<th>含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdffile" data-raw-source="[IWDFFile](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-iwdffile)">IWDFFile</a></p></td>
<td><p>pClientFile</p></td>
<td><p>此 UMDF COM 接口表示平台与客户端应用程序关联的文件对象。 虽然传感器方法调用始终将此类型提供为有效的接口指针，但它旨在用作应用程序的 ID。 指针包含的地址是可以标识客户端应用程序的唯一编号。 请注意，此值不同于指针本身的地址。 不要使用地址操作员 ( # A0) 来检索 ID。 使用指针本身。</p>
<p>如果选择使用此指针来访问基础对象，请记得先通过指针调用 AddRef，并在完成后调用发布。</p></td>
</tr>
<tr class="even">
<td><p><strong>LPWSTR</strong></p></td>
<td><p>pwszSensorID</p></td>
<td><p>此字符串是由特定传感器的驱动程序提供的唯一 ID。 对于特定设备上的每个传感器，此 ID 必须是唯一的。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/portabledevicetypes/nn-portabledevicetypes-iportabledevicevalues" data-raw-source="[IPortableDeviceValues](/windows-hardware/drivers/ddi/portabledevicetypes/nn-portabledevicetypes-iportabledevicevalues)">IPortableDeviceValues</a></p></td>
<td><p>ppDataValues</p>
<p>ppPropertyValues</p>
<p>pPropertiesToSet</p>
<p>ppResults</p></td>
<td><p>此 WPD 接口提供一种简便的方法来创建名称/值对的属性包。 <strong>PROPERTYKEY</strong>表示名称， <strong>PROPVARIANT</strong>表示值。 DDI 使用此接口来设置和检索值集或单个值。</p>
<p>如果需要新的对象，可以通过使用 <strong>CLSID_PortableDeviceValues</strong>调用 CoCreateInstance，从方法检索此接口。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/portabledevicetypes/nn-portabledevicetypes-iportabledevicevaluescollection" data-raw-source="[IPortableDeviceValuesCollection](/windows-hardware/drivers/ddi/portabledevicetypes/nn-portabledevicetypes-iportabledevicevaluescollection)">IPortableDeviceValuesCollection</a></p></td>
<td><p>pEventCollection</p>
<p>ppSensorObjectCollection</p></td>
<td><p>此 WPD 接口包含 <a href="/windows-hardware/drivers/ddi/portabledevicetypes/nn-portabledevicetypes-iportabledevicevalues" data-raw-source="[IPortableDeviceValues](/windows-hardware/drivers/ddi/portabledevicetypes/nn-portabledevicetypes-iportabledevicevalues)">IPortableDeviceValues</a> 对象的集合。 使用此接口的 DDI 方法使你能够同时提供多个数据集，例如多个事件或多个传感器的相关信息。</p>
<p>如果需要新的对象，可以通过使用 <strong>CLSID_PortableDeviceValuesCollection</strong>调用 CoCreateInstance，从方法检索此接口。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/portabledevicetypes/nn-portabledevicetypes-iportabledevicekeycollection" data-raw-source="[IPortableDeviceKeyCollection](/windows-hardware/drivers/ddi/portabledevicetypes/nn-portabledevicetypes-iportabledevicekeycollection)">IPortableDeviceKeyCollection</a></p></td>
<td><p>pDataFields</p>
<p>pProperties</p>
<p>ppSupportedDataFields</p>
<p>ppSupportedProperties</p></td>
<td><p>此 WPD 接口包含 <strong>PROPERTYKEY</strong>的集合。 这些键表示可以由 <a href="/windows-hardware/drivers/ddi/portabledevicetypes/nn-portabledevicetypes-iportabledevicevalues" data-raw-source="[IPortableDeviceValues](/windows-hardware/drivers/ddi/portabledevicetypes/nn-portabledevicetypes-iportabledevicevalues)">IPortableDeviceValues</a>存储的属性名称。 DDI 使用此集合对象来设置和检索属性名称集或单个名称。</p>
<p>如果需要新的对象，可以通过使用 <strong>CLSID_PortableDeviceKeyCollection</strong>调用 CoCreateInstance，从方法检索此接口。</p></td>
</tr>
</tbody>
</table>

