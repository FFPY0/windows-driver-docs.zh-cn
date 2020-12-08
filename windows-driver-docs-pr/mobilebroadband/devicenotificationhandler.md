---
title: DeviceNotificationHandler
description: DeviceNotificationHandler
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bde41065f035e6fda81d6fac513ace225258c852
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788553"
---
# <a name="devicenotificationhandler"></a>DeviceNotificationHandler

[!include[MBAE deprecation warning](../includes/mbae-deprecation-warning.md)]

DeviceNotificationHandler 元素指定设备通知处理程序。 设备通知处理程序允许您运行代码来响应事件，例如移动网络操作员管理 SMS 或 USSD 通知，即使 Microsoft Store 应用程序未运行也是如此。 有关实现通知处理程序的详细信息，请参阅 [移动运营商通知](./enabling-mobile-operator-notifications-and-system-events.md) 白皮书。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<DeviceNotificationHandler EventID=”xs:string” EventAsset=”xs:string”/>
```

## <a name="span-idattributesspanspan-idattributesspanspan-idattributesspanattributes"></a><span id="Attributes"></span><span id="attributes"></span><span id="ATTRIBUTES"></span>属性


<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>Attribute</th>
<th>类型</th>
<th>必须</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EventID</p></td>
<td><p>xs:string</p></td>
<td><p>是</p></td>
<td><p>设备通知处理程序的事件 ID。</p></td>
</tr>
<tr class="even">
<td><p>EventAsset</p></td>
<td><p>xs:string</p></td>
<td><p>是</p></td>
<td><p>设备通知处理程序的事件资产。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idchild_elementsspanspan-idchild_elementsspanspan-idchild_elementsspanchild-elements"></a><span id="Child_elements"></span><span id="child_elements"></span><span id="CHILD_ELEMENTS"></span>子元素


没有任何子元素。

## <a name="span-idparent_elementsspanspan-idparent_elementsspanspan-idparent_elementsspanparent-elements"></a><span id="Parent_elements"></span><span id="parent_elements"></span><span id="PARENT_ELEMENTS"></span>父元素


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>元素</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="devicenotificationhandlers.md" data-raw-source="[DeviceNotificationHandlers](devicenotificationhandlers.md)">DeviceNotificationHandlers</a></p></td>
<td><p>指定设备通知处理程序。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


``` syntax
<xs:element name="DeviceNotificationHandler" type="tns:DeviceNotificationHandlerType" maxOccurs="unbounded" />

<xs:complexType name="DeviceNotificationHandlerType">
  <xs:attribute name="EventID" type="xs:string" use="required"/>
  <xs:attribute name="EventAsset" type="xs:string" use="required"/>
</xs:complexType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


-   在 [应用程序](application-softwareinfo-schema.md) 元素中指定 DeviceNotificationHandler 时，系统会调用事件处理程序，并在设备更改为状态时调用事件。

-   **EventID** 特性是 SMS 设备用例的 SMSEventHandler。

-   **EventAsset** 属性的值与你在应用程序清单中指定为 BackgroundTasks 的扩展的值相同。

DeviceNotificationHandler 元素是可选的。

 

