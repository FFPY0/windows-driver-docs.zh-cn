---
title: 标识 (SoftwareInfo)
description: 标识 (SoftwareInfo)
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5514763df5b508090acffd56327880a95699e644
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788493"
---
# <a name="identity-softwareinfo"></a>标识 (SoftwareInfo)

[!include[MBAE deprecation warning](../includes/mbae-deprecation-warning.md)]

标识元素指定应用程序的发布服务器标识和应用程序清单名称。

## <a name="span-idusagespanspan-idusagespanspan-idusagespanusage"></a><span id="Usage"></span><span id="usage"></span><span id="USAGE"></span>使用情况


``` syntax
<Identity Name=”tns:AsciiIdentifierType” Publisher=”tns:DistinguishedNameType” />
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
<td><p>“属性”</p></td>
<td><p>tns： AsciiIdentifierType</p></td>
<td><p>是</p></td>
<td><p>应用程序清单文件中指定的应用程序的名称。</p></td>
</tr>
<tr class="even">
<td><p>Publisher</p></td>
<td><p>tns： DistinguishedNameType</p></td>
<td><p>是</p></td>
<td><p>应用程序的发布者标识。</p></td>
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
<td><p><a href="devicecompanionapplications.md" data-raw-source="[DeviceCompanionApplications](devicecompanionapplications.md)">DeviceCompanionApplications</a></p></td>
<td><p>指定在计算机上检测到操作员的移动宽带硬件时要下载的应用。</p></td>
</tr>
</tbody>
</table>

 

## <a name="span-idxsdspanspan-idxsdspanxsd"></a><span id="XSD"></span><span id="xsd"></span>XSD.EXE


``` syntax
<xs:element name="Identity" type="tns:IdentityType" />

<xs:complexType name="IdentityType">
  <xs:attribute name="Name" type="tns:PackageNameType" use="required"/>
  <xs:attribute name="Publisher" type="tns:PublisherType" use="required"/>
</xs:complexType>

<xs:simpleType name="PackageNameType">
  <xs:restriction base="tns:AsciiIdentifierType">
    <xs:minLength value="3"/>
    <xs:maxLength value="50"/>
  </xs:restriction>
</xs:simpleType>

<xs:simpleType name="PublisherType">
  <xs:restriction base="tns:DistinguishedNameType">
    <xs:maxLength value="8192"/>
  </xs:restriction>
</xs:simpleType>

<xs:simpleType name="AsciiIdentifierType">
  <xs:restriction base="tns:AllowedAsciiCharSetType">
    <xs:pattern value="[^_ ]+"/>
  </xs:restriction>
</xs:simpleType>

<xs:simpleType name="DistinguishedNameType">
  <xs:restriction base="tns:NonEmptyStringType">
    <xs:pattern value="(CN|L|O|OU|E|C|S|STREET|T|G|I|SN|DC|SERIALNUMBER|(OID\.(0|[1-9][0-9]*)(\.(0|[1-9][0-9]*))+))=(([^,+="&lt;&gt;#;])+|".*")(, ((CN|L|O|OU|E|C|S|STREET|T|G|I|SN|DC|SERIALNUMBER|(OID\.(0|[1-9][0-9]*)(\.(0|[1-9][0-9]*))+))=(([^,+="&lt;&gt;#;])+|".*")))*"/>
  </xs:restriction>
</xs:simpleType>

<xs:simpleType name="NonEmptyStringType">
  <xs:restriction base="xs:string">
    <xs:minLength value="1"/>
    <xs:maxLength value="32767"/>
    <xs:pattern value="[^\s]|([^\s].*[^\s])"/>
  </xs:restriction>
</xs:simpleType>

<xs:simpleType name="AllowedAsciiCharSetType">
  <xs:restriction base="tns:NonEmptyStringType">
    <xs:pattern value="[-_. A-Za-z0-9]+"/>
  </xs:restriction>
</xs:simpleType>
```

## <a name="span-idremarksspanspan-idremarksspanspan-idremarksspanremarks"></a><span id="Remarks"></span><span id="remarks"></span><span id="REMARKS"></span>备注


Identity 元素是可选的。

 

 





