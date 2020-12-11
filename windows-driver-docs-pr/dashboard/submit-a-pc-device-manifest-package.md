---
title: 提交电脑设备清单包
description: 提交电脑设备清单包
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e142b9bda595dc89aa466eecdb7f86ef857d497c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800277"
---
# <a name="submit-a-pc-device-manifest-package"></a>提交电脑设备清单包

## <a name="submitting-a-pc-device-manifest-package"></a>提交电脑设备清单包

你可以使用相同的方法提交用于预览或发布的包。

### <a name="to-submit-a-device-manifest-package"></a>提交设备清单包

1. 使用 [SignTool](/windows/win32/seccrypto/signtool) 工具对 devicemanifest-ms 程序包进行签名。

2. 从硬件开发人员中心或 Windows 开发人员中心，使用 Microsoft 帐户登录到“仪表板”  。

3. 在“设备元数据”  下，单击“创建体验”  （如果你希望提交新体验），或单击“管理体验”  （如果你希望修改现有体验）。

4. 浏览并选择你的新 devicemanifest-ms 程序包，然后单击“提交”  。

## <a name="creating-a-device-manifest-submission-package"></a>创建设备清单提交程序包

设备清单提交程序包是所有电脑设备元数据包提交到硬件开发人员中心时必须采用的格式。

设备清单提交程序包包含声明区域设置支持和能够验证电脑 HWID 属于正在进行提交公司的文件。 设备清单包还包含设备元数据包。

设备清单提交程序包采用与设备元数据包相同的方式上载到硬件开发人员中心。 使用相同的用户界面和上传框，输入要上传的 \*.devicemanifest-ms 文件的名称。

硬件开发人员中心用户界面上批量上载以外的所有文件上载框都将接受设备清单提交程序包。

### <a name="device-manifest-submission-package-contents"></a>设备清单提交程序包内容

每个设备清单提交包都包含以下组成部分：

- **设备元数据包**

    此包包含用于在 Windows 中显示设备图标、设置操作及使用设备体验功能的信息和图片。

    设备元数据包始终必需。

- **LocaleInfo XML 文档**

    此文档包含有关包含在附带设备元数据包中的区域设置的数据。 硬件开发人员中心使用此数据来正确验证一个或多个区域设置的设备元数据包。

    LocaleInfo XML 文档始终是必需的，即使设备元数据包仅包含单个区域设置。

- **PcMetadataSubmission XML 文档**

    此文档包含用于验证附带的电脑设备元数据包中的 HWID 的数据。 硬件开发人员中心使用此数据来验证设备元数据包中的 HWID 是否属于正确的公司。

    PcMetadataSubmission XML 文档仅对电脑设备元数据包是必需的。

>[!NOTE]
>这些 XML 文档必须使用 UTF-8 编码进行保存。

### <a name="structure-of-a-pc-device-manifest-submission-package"></a>电脑设备清单提交包的结构

设备清单包的结构取决于包含的设备元数据用于电脑、用于移动宽带还是包含对多个区域设置的支持。

如果设备元数据不属于这三个类别中的任何一个，则不需要设备清单包。 但是，设备清单包仍然可用于指示设备元数据包是用于单个区域设置的。

电脑设备清单提交包的组成部分存储在压缩的 Cab 文件中。 该文件名必须具有后缀 .devicemanifest-ms。

每个电脑设备清单提交包都必须具有以下结构：

``` syntax
GUID1.devicemanifest-ms
  \GUID1.devicemetadata-ms
  \LocaleInfo.xml
  \PcMetadataSubmission.xml
```

“GUID1”必须是一个 GUID。

若要创建 LocaleInfo.xml 和 PcMetadataSubmission.xml，请参阅以下内容。

若要了解如何开发设备元数据包 \*.devicemetadata-ms，请参阅 [Windows 8 的设备元数据包架构参考](/previous-versions/windows/hardware/metadata/dn465877(v=vs.85))

你可以使用 Cabarc 工具创建这些 CAB 程序包。 有关此工具的详细信息，请参阅 [Cabarc 概述](/previous-versions/windows/it-pro/windows-server-2003/cc781787(v=ws.10))

使用 Cabarc 工具创建 \*.devicemanifest-ms 文件时，必须创建一个本地目录，其中设备元数据包 (\*.devicemetadata-ms)、LocaleInfo XML 文档和 PcMetadataSubmission XML 文档位于该目录的根目录中。

#### <a name="remarks-device-manifest"></a>备注（设备清单）

- .devicemanifest-ms 和 .devicemetadata-ms 文件名必须指定不带花括号 ({}) 分隔符的 GUID。

- 每个电脑设备清单提交和设备元数据包的 GUID 都必须唯一。 当你创建新的或修改的程序包时，必须创建新 GUID。

- 有关如何创建 cabinet 文件的详细信息，请参阅 [Microsoft Cabinet 软件开发工具包](/previous-versions/ms974336(v=msdn.10))。

#### <a name="example-device-manifest"></a>示例（设备清单）

下面显示了如何使用 Cabarc 工具创建 .devicemanifest-ms 文件的示例。 在此示例中，电脑设备清单文件的组成部分位于名为 PcPackages 的本地目录中：

``` syntax
.\PcPackages\
.\PcPackages\PcMetadataSubmission.xml
.\PcPackages\LocaleInfo.xml
.\PcPackages\GUID.devicemetadata-ms
```

GUID.devicemanifest-ms 文件在名为 PCFiles 的本地目录中创建：

``` syntax
Cabarc.exe -r -p -P  .\PcPackages\
N .\PCFiles\ GUID.devicemanifest-ms
.\PcPackages\PcMetadataSubmission.xml
.\PcPackages\LocaleInfo.xml
```

有关此工具的详细信息，请参阅 [Cabarc 概述](/previous-versions/windows/it-pro/windows-server-2003/cc781787(v=ws.10))。

## <a name="creating-pcmetadatasubmissionxml"></a>创建 PcMetadataSubmission.xml

### <a name="pcmetadatasubmission-xml-schema"></a>PcMetadataSubmission XML 架构

设备清单提交程序包可包含一个 PcMetadataSubmission.xml 文档，其中包含硬件开发人员中心站点用于验证 PackageInfo.xml 中的计算机硬件 ID 的信息。

PcMetadataSubmission.xml 文档中的数据基于 PcMetadataSubmission XML 架构（将在下面进行介绍）设置格式。

>[!NOTE]
>该 XML 文档必须使用 UTF-8 编码进行保存。

有关 ComputerHardwareID 的详细信息，请参阅[如何创建设备和打印机的设备元数据包](/previous-versions/windows/hardware/metadata/dn465877(v=vs.85))。

#### <a name="pcmetadatasubmission-xml-schema-namespace"></a>PcMetadataSubmission XML 架构命名空间

以下是 PcMetadataSubmission XML 架构的命名空间：

- `http://schemas.microsoft.com/Windows/2009/05/MetadataSubmission/PcMetadataSubmission`

- `http://schemas.microsoft.com/Windows/2011/06/MetadataSubmission/PcMetadataSubmissionv2`

#### <a name="overview-of-pcmetadatasubmission-xml-elementsattributes"></a>PcMetadataSubmission XML 元素/属性概述

下表描述 PcMetadataSubmission XML 架构的元数据元素和属性。

|元素/属性|元素/属性类型|必需/可选|说明|
|----|----|----|----|
|SMBIOSEntry|SMBIOSEntryType|必需|指定计算机的 SMBIOS 信息。|
|SystemManufacturer|tns:SMBIOSStringType|必需|指定计算机的名称。|
|SystemFamily|tns:SMBIOSStringType|可选|指定计算机制造商的系列名称。|
|SystemProductName|tns:SMBIOSStringType|可选|指定产品（计算机）的名称。|
|BIOSVendor|tns:SMBIOSStringType|可选|指定 BIOS 制造商的名称。|
|BIOSVersion|tns:SMBIOSStringType|可选|指定 BIOS 的版本号。|
|SystemBIOSMajorRelease|tns:BIOSReleaseType|可选|指定 BIOS 的 MajorRelease 版本。|
|SystemBIOSMinorRelease|tns:BIOSReleaseType|可选|指定 BIOS 的 MinorRelease 版本。|
|Enclosuretype|tns:TypeofEnclosureType|可选|指定计算机的机箱类型。|
|SKUNumber|v2:SMBIOSStringType|可选|指定计算机的 SKU 号。|

#### <a name="pcmetadatasubmission-xml-schema-definition"></a>PcMetadataSubmission XML 架构定义

以下是 PcMetadataSubmission XML 架构定义：

``` syntax
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema targetNamespace="http://schemas.microsoft.com/Windows/2009/05/MetadataSubmission/PcMetadataSubmission" xmlns:tns="http://schemas.microsoft.com/Windows/2009/05/MetadataSubmission/PcMetadataSubmission" xmlns:xs="http://www.w3.org/2001/XMLSchema" xmlns:v2="http://schemas.microsoft.com/Windows/2011/06/MetadataSubmission/PcMetadataSubmissionv2" elementFormDefault="qualified" blockDefault="#all">

  <xs:element name="PcMetadataSubmission" type="tns:PcMetadataSubmissionType" />
  <xs:complexType name="PcMetadataSubmissionType">
    <xs:sequence>
      <xs:element name="SMBIOSList" type="tns:SMBIOSListType" />
      <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
    </xs:sequence>
  </xs:complexType>

  <xs:complexType name="SMBIOSListType">
    <xs:sequence>
      <xs:element name="SMBIOSEntry" type="tns:SMBIOSEntryType" maxOccurs="unbounded" />
      <xs:any namespace="##other" processContents="lax" minOccurs="0" maxOccurs="unbounded" />
    </xs:sequence>
  </xs:complexType>

  <xs:complexType name="SMBIOSEntryType">
    <xs:simpleContent>
      <xs:extension base="xs:string">
        <xs:attribute name="SystemManufacturer" type="tns:SMBIOSStringType" use="required" />
        <xs:attribute name="SystemFamily" type="tns:SMBIOSStringType" use="optional" />
        <xs:attribute name="SystemProductName" type="tns:SMBIOSStringType" use="optional" />
        <xs:attribute name="BIOSVendor" type="tns:SMBIOSStringType" use="optional" />
        <xs:attribute name="BIOSVersion" type="tns:SMBIOSStringType" use="optional" />
        <xs:attribute name="SystemBIOSMajorRelease" type="tns:BIOSReleaseType" use="optional" />
        <xs:attribute name="SystemBIOSMinorRelease" type="tns:BIOSReleaseType" use="optional" />
        <xs:attribute name="EnclosureType" type="tns:TypeofEnclosureType" use="optional" />
        <xs:attribute ref="v2:SKUNumber" use="optional" />
      </xs:extension>
    </xs:simpleContent>
  </xs:complexType>
  <xs:simpleType name="SMBIOSStringType">
    <xs:restriction base="xs:string">
      <xs:minLength value="1" />
      <xs:maxLength value="64" />
    </xs:restriction>
  </xs:simpleType>
  <xs:simpleType name="BIOSReleaseType">
    <xs:restriction base="xs:hexBinary">
      <xs:minLength value="1" />
      <xs:maxLength value="1" />
    </xs:restriction>
  </xs:simpleType>
  <xs:simpleType name="TypeofEnclosureType">
    <xs:restriction base="xs:hexBinary">
      <xs:pattern value="([0-7][0-9A-F]|0[0-9A-F])" />
    </xs:restriction>
  </xs:simpleType>
</xs:schema>
```

以下是 PcMetadataSubmissionv2 XML 架构定义：

``` syntax
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema targetNamespace="http://schemas.microsoft.com/Windows/2011/06/MetadataSubmission/PcMetadataSubmissionv2" xmlns:tns="http://schemas.microsoft.com/Windows/2011/06/MetadataSubmission/PcMetadataSubmissionv2" xmlns:xs="http://www.w3.org/2001/XMLSchema" elementFormDefault="qualified" blockDefault="#all">

  <xs:attribute name="SKUNumber" type="tns:SMBIOSStringType" />

  <xs:simpleType name="SMBIOSStringType">
    <xs:restriction base="xs:string">
      <xs:minLength value="1" />
      <xs:maxLength value="64" />
    </xs:restriction>
  </xs:simpleType>

</xs:schema>
```

#### <a name="pcmetadatasubmission-xml-schema-reference"></a>PcMetadataSubmission XML 架构参考

PcMetadataSubmission XML 架构定义以下元素和属性：

- SMBIOSList
  - SMBIOSEntry
    - SystemManufacturer
    - SystemFamily
    - SystemProductName
    - BIOSVendor
    - BIOSVersion
    - SystemBIOSMajorRelease
    - SystemBIOSMinorRelease
    - Enclosuretype
    - SKUNumber

### <a name="smbiosentry-elements"></a>SMBIOSEntry 元素

SMBIOSEntry 元素指定计算机系统信息。 硬件开发人员中心将基于此信息创建计算机硬件 ID，并将该值与你随 PcMetadataSubmission.xml 一起提交的 packageinfo.xml 中的计算机硬件 ID 进行比较。

``` syntax
<xs:element name="SMBIOSEntry" type="tns:SMBIOSEntryType" maxOccurs="unbounded" />

<xs:complexType name="SMBIOSEntryType">
    <xs:simpleContent>
      <xs:extension base="xs:string">
        <xs:attribute name="SystemManufacturer" type="tns:SMBIOSStringType" use="required" />
        <xs:attribute name="SystemFamily" type="tns:SMBIOSStringType" use="optional" />
        <xs:attribute name="SystemProductName" type="tns:SMBIOSStringType" use="optional" />
        <xs:attribute name="BIOSVendor" type="tns:SMBIOSStringType" use="optional" />
        <xs:attribute name="BIOSVersion" type="tns:SMBIOSStringType" use="optional" />
        <xs:attribute name="SystemBIOSMajorRelease" type="tns:BIOSReleaseType" use="optional" />
        <xs:attribute name="SystemBIOSMinorRelease" type="tns:BIOSReleaseType" use="optional" />
        <xs:attribute name="Enclosuretype" type="tns:TypeofEnclosureType" use="optional" />
        <xs:anyAttribute namespace="##other" processContents="lax" />
      </xs:extension>
    </xs:simpleContent>
  </xs:complexType>
```

#### <a name="remarks-smbiosentry-element"></a>备注（SMBIOSEntry 元素）

可以使用多个 SMBIOSEntry 元素指定多个系统。

例如，考虑元数据包支持多个电脑系统。 可以使用以下 SMBIOSEntry 元素定义电脑系统。

``` syntax
<SMBIOSList>
  <SMBIOSEntry
      SystemManufacturer="FABRIKAM" SystemFamily…
  />
  <SMBIOSEntry
      SystemManufacturer="FABRIKAM" SystemFamily…
</SMBIOSList>
```

### <a name="systemmanufacturer-attributes"></a>SystemManufacturer 属性

SystemManufacturer 属性指定计算机的系列名称。

``` syntax
<xs:attribute name="SystemManufacturer" type="tns:SMBIOSStringType" use="required" />

<xs:simpleType name="SMBIOSStringType">
  <xs:restriction base="xs:string">
    <xs:minLength value="1" />
    <xs:maxLength value="64" />
  </xs:restriction>
</xs:simpleType>
```

#### <a name="remarks-systemmanufacturer-attributes"></a>备注（SystemManufacturer 属性）

SystemManufacturer 属性指定的值必须与目标电脑 SMBIOS 表中“制造商”字段中的值相同。 下表显示了 SMBIOS 中“制造商”字段的字段信息。

|字段名称|结构名称和类型|SMBIOS 规范版本|偏移量|长度|值|说明|
|----|----|----|----|----|----|----|----|
|制造商|系统信息(类型 1)|2.0+|04h|BYTE|STRING|dmiStrucBuffer 数组中以 Null 结尾的字符串的索引。 此字符串指定计算机制造商的名称。|

有关 dmiStrucBuffer 数组和 SMBIOS 字段的详细信息，请参阅[系统管理 BIOS (SMBIOS) 规范](https://go.microsoft.com/fwlink/p/?LinkId=145867)。

### <a name="systemfamily-attributes"></a>SystemFamily 属性

SystemFamily 属性指定计算机制造商的名称。

``` syntax
<xs:attribute name="SystemFamily" type="tns:SMBIOSStringType" use="optional" />

<xs:simpleType name="SMBIOSStringType">
  <xs:restriction base="xs:string">
    <xs:minLength value="1" />
    <xs:maxLength value="64" />
  </xs:restriction>
</xs:simpleType>
```

#### <a name="remarks-systemfamily-attributes"></a>备注（SystemFamily 属性）

SystemFamily 属性指定的值必须与目标电脑 SMBIOS 表中“系列”字段中的值相同。 下表显示了 SMBIOS 中“系列”字段的字段信息。

|字段名称|结构名称和类型|SMBIOS 规范版本|偏移量|长度|值|说明|
|----|----|----|----|----|----|----|
|家庭|系统信息(类型 1)|2.4+|1Ah|BYTE|STRING|dmiStrucBuffer 数组中以 Null 结尾的字符串的索引。 此字符串指定特定计算机所属的系列。系列指从硬件或软件的视角来看相似但不完全相同的一组计算机。通常，一个系列由不同的计算机型号组成，而这些型号具有不同的配置和价格点。 同一系列中的计算机通常具有相似的品牌和外观特点。|

有关 dmiStrucBuffer 数组和 SMBIOS 字段的详细信息，请参阅[系统管理 BIOS (SMBIOS) 规范](https://go.microsoft.com/fwlink/p/?LinkId=145867)。

### <a name="systemproductname-attributes"></a>SystemProductName 属性

SystemProductName 属性指定产品（计算机）的名称。

``` syntax
<xs:attribute name="SystemProductName" type="tns:SMBIOSStringType" use="optional" />

<xs:simpleType name="SMBIOSStringType">
  <xs:restriction base="xs:string">
    <xs:minLength value="1" />
    <xs:maxLength value="64" />
  </xs:restriction>
</xs:simpleType>
```

#### <a name="remarks-systemproductname-attribute"></a>备注（SystemProductName 属性）

SystemProductName 属性指定的值必须与目标电脑 SMBIOS 表中“产品名称”字段中的值相同。 下表显示了 SMBIOS 中“产品名称”字段的字段信息。

|字段名称|结构名称和类型|SMBIOS 规范版本|偏移量|长度|值|说明|
|----|----|----|----|----|----|----|
|产品名称|系统信息(类型 1)|2.0+|05h|BYTE|STRING|dmiStrucBuffer 数组中以 Null 结尾的字符串的索引。 此字符串指定计算机的产品名称。|

有关 dmiStrucBuffer 数组和 SMBIOS 字段的详细信息，请参阅[系统管理 BIOS (SMBIOS) 规范](https://go.microsoft.com/fwlink/p/?LinkId=145867)。

### <a name="biosvendor-attributes"></a>BIOSVendor 属性

BIOSVendor 属性指定 BIOS 制造商的名称。

``` syntax
<xs:attribute name="BIOSVendor" type="tns:SMBIOSStringType" use="optional" />

<xs:simpleType name="SMBIOSStringType">
  <xs:restriction base="xs:string">
    <xs:minLength value="1" />
    <xs:maxLength value="64" />
  </xs:restriction>
</xs:simpleType>
```

#### <a name="remarks-biosvendor-attribute"></a>备注（BIOSVendor 属性）

BIOSVendor 属性指定的值必须与目标电脑 SMBIOS 表中“供应商”字段中的值相同。 下表显示了 SMBIOS 中“供应商”字段的字段信息。

|字段名称|结构名称和类型|SMBIOS 规范版本|偏移量|长度|值|说明|
|----|----|----|----|----|----|----|
|供应商|BIOS 信息(类型 0)|2.0|04h|BYTE|STRING|dmiStrucBuffer 数组中以 Null 结尾的字符串的索引。 此字符串指定 BIOS 供应商的名称。|

有关 dmiStrucBuffer 数组和 SMBIOS 字段的详细信息，请参阅[系统管理 BIOS (SMBIOS) 规范](https://go.microsoft.com/fwlink/p/?LinkId=145867)。

### <a name="biosversion-attributes"></a>BIOSVersion 属性

BIOSVersion 属性指定 BIOS 的版本号。

``` syntax
<xs:attribute name="BIOSVersion" type="tns:SMBIOSStringType" use="optional" />

<xs:simpleType name="SMBIOSStringType">
  <xs:restriction base="xs:string">
    <xs:minLength value="1" />
    <xs:maxLength value="64" />
  </xs:restriction>
</xs:simpleType>
```

#### <a name="remarks-biosversion-attribute"></a>备注（BIOSVersion 属性）

BIOSVersion 属性指定的值必须与目标电脑 SMBIOS 表中“BIOS 版本”字段中的值相同。 下表显示了 SMBIOS 中“BIOS 版本”字段的字段信息。

|字段名称|结构名称和类型|SMBIOS 规范版本|偏移量|长度|值|说明|
|----|----|----|----|----|----|----|
|BIOS 版本|BIOS 信息(类型 0)|2.0|05h|BYTE|STRING|dmiStrucBuffer 数组中以 Null 结尾的字符串的索引。 此字符串包含有关处理器核心和 OEM 版本的信息。|

有关 dmiStrucBuffer 数组和 SMBIOS 字段的详细信息，请参阅[系统管理 BIOS (SMBIOS) 规范](https://go.microsoft.com/fwlink/p/?LinkId=145867)。

### <a name="systembiosmajorrelease-attributes"></a>SystemBIOSMajorRelease 属性

SystemBIOSMajorRelease 属性指定 BIOS 的主要发行版本。

``` syntax
<xs:attribute name="SystemBIOSMajorRelease" type="tns:BIOSReleaseType" use="optional" />

<xs:simpleType name="BIOSReleaseType">
  <xs:restriction base="xs:hexBinary">
    <xs:minLength value="1" />
    <xs:maxLength value="1" />
  </xs:restriction>
</xs:simpleType>
```

#### <a name="remarks-systembiosmajorrelease-attribute"></a>备注（SystemBIOSMajorRelease 属性）

SystemBIOSMajorRelease 属性指定的值必须与目标电脑 SMBIOS 表中 SystemBIOSMajorRelease 字段中的值相同。 下表显示了 SMBIOS 中 SystemBIOSMajorRelease 字段的字段信息。

|字段名称|结构名称和类型|SMBIOS 规范版本|偏移量|长度|值|说明|
|----|----|----|----|----|----|----|
|系统 BIOS 主要版本|BIOS 信息(类型 0)|2.4|14h|BYTE|视情况而定。|系统 BIOS 的主要版本。|

有关 SMBIOS 字段的详细信息，请参阅[系统管理 BIOS (SMBIOS) 规范](https://go.microsoft.com/fwlink/p/?LinkId=145867)。

### <a name="systembiosminorrelease-attributes"></a>SystemBIOSMinorRelease 属性

SystemBIOSMinorRelease 属性指定 BIOS 的次要发行版本。

``` syntax
<xs:attribute name="SystemBIOSMinorRelease" type="tns:BIOSReleaseType" use="optional" />

<xs:simpleType name="BIOSReleaseType">
  <xs:restriction base="xs:hexBinary">
    <xs:minLength value="1" />
    <xs:maxLength value="1" />
  </xs:restriction>
</xs:simpleType>
```

#### <a name="remarks-systembiosminorrelease-attributes"></a>备注（SYSTEMBIOSMinorRelease 属性）

SystemBIOSMinorRelease 属性指定的值必须与目标电脑 SMBIOS 表中 SystemBIOSMinorRelease 字段中的值相同。 下表显示了 SMBIOS 中 SystemBIOSMinorRelease 字段的字段信息。

|字段名称|结构名称和类型|SMBIOS 规范版本|偏移量|长度|值|说明|
|----|----|----|----|----|----|----|
|系统 BIOS 次要版本|BIOS 信息(类型 0)|2.4|15h|BYTE|视情况而定。|系统 BIOS 的次要版本。|

有关 SMBIOS 字段的详细信息，请参阅[系统管理 BIOS (SMBIOS) 规范](https://go.microsoft.com/fwlink/p/?LinkId=145867)。

### <a name="enclosuretype-attribute"></a>Enclosuretype 属性

Enclosuretype 属性指定计算机的机箱类型。

``` syntax
<xs:attribute name="EnclosureType" type="tns:TypeofEnclosureType" use="optional" />

<xs:simpleType name="TypeofEnclosureType">
  <xs:restriction base="xs:hexBinary">
    <xs:pattern value="([0-7][0-9A-F]|0[0-9A-F])" />
  </xs:restriction>
</xs:simpleType>
```

#### <a name="remarks-enclosuretype-attribute"></a>备注（Enclosuretype 属性）

Enclosuretype 属性指定的值必须与目标电脑 SMBIOS 表中“机箱”字段中的值相同。 下表显示了 SMBIOS 中“机箱”字段的字段信息。

|字段名称|结构名称和类型|SMBIOS 规范版本|偏移量|长度|值|说明|
|----|----|----|----|----|----|----|
|机箱类型|系统机箱(类型 3)|2.0+|05h|BYTE|视情况而定。|系统机箱或机壳类型。|

有关 SMBIOS 字段的详细信息，请参阅[系统管理 BIOS (SMBIOS) 规范](https://go.microsoft.com/fwlink/p/?LinkId=145867)。

### <a name="skunumber-element"></a>SKUNumber 元素

SKUNumber 元素指定计算机的 SKU 号。

``` syntax
<xs:attribute name="SKUNumber" type="tns:SMBIOSStringType" />

<xs:simpleType name="SMBIOSStringType">
  <xs:restriction base="xs:string">
    <xs:minLength value="1" />
    <xs:maxLength value="64" />
  </xs:restriction>
</xs:simpleType>
```

#### <a name="remarks-skunumber-element"></a>备注（SKUNumber 元素）

SKUNumber 元素指定的值必须与目标电脑 SMBIOS 表中“SKU 号”字段中的值相同。 下表显示了 SMBIOS 中“SKU 号”字段的字段信息。

|字段名称|结构名称和类型|SMBIOS 规范版本|偏移量|长度|值|说明|
|----|----|----|----|----|----|----|
|SKU 号|系统信息(类型 1)|2.4+|19h|BYTE|STRING|以 Null 结尾的字符串编号。此文本字符串用于标识销售的特定计算机配置。 有时也将它称为产品 ID 或采购订单号。 此编号通常会在现有字段中找到，但是没有标准格式。 通常，对于给定 OEM 的给定系统板，会有数十个独特的处理器、内存、硬盘驱动器和光驱配置。|

有关 SMBIOS 字段的详细信息，请参阅[系统管理 BIOS (SMBIOS) 规范](https://go.microsoft.com/fwlink/p/?LinkId=145867)。

### <a name="pcmetadatasubmission-xml-example"></a>PcMetadataSubmission XML 示例

以下 XML 文档使用 PcMetadataSubmission XML 架构来指定目标计算机的 PcMetadataSubmission 信息的组成部分。

``` syntax
<?xml version="1.0" encoding="utf-8"?>
<PcMetadataSubmission xmlns="http://schemas.microsoft.com/Windows/2009/05/MetadataSubmission/PcMetadataSubmission">
  <SMBIOSList>
   <SMBIOSEntry
      SystemManufacturer="FABRIKAM"
      SystemFamily="FABRIKAM A SERIES"
      SystemProductName="FABRIKAM LAPTOP"
      BIOSVendor="FABRIKAM"
      BIOSVersion="7BETC7WW (2.08 )"
      SystemBIOSMajorRelease="08"
      SystemBIOSMinorRelease="00"
      EnclosureType="0A"
      v2:SKUNumber="1234567890ABCD"
    />
  </SMBIOSList>
</PcMetadataSubmission>
```

## <a name="creating-localeinfoxml"></a>创建 LocaleInfo.xml

有关创建用于提交的 Localeinfo.xml 文件的信息，请参阅[创建 LocaleInfo.xml 提交文件](create-the-localeinfoxml-submission-file.md)。
