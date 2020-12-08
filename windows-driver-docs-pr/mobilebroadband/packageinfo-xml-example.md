---
title: PackageInfo XML 示例
description: PackageInfo XML 示例
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5f40465563590125c79b2359d784bfb8a7b47cbc
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786239"
---
# <a name="packageinfo-xml-example"></a>PackageInfo XML 示例

[!include[MBAE deprecation warning](../includes/mbae-deprecation-warning.md)]

下面的 XML 文档使用 [PACKAGEINFO xml 架构](packageinfo-xml-schema.md) 来指定供应商的元数据包的组件。

包适用于具有以下硬件 ID 的服务：

MBAE:0:L9@E}} DT2。 \*F65MQA57Y + L

>[!NOTE]
>PackageInfo.xml 中包含的硬件 Id 必须将 "DOID：" 前缀添加到其中。

包还用于 EN-US 区域设置，该区域设置将文档设置为元数据包组件的默认区域设置。

``` syntax
<?xml version="1.0" encoding ="UTF-8" ?>

  <PackageInfo xmlns=http://schemas.microsoft.com/windows/DeviceMetadata/PackageInfo/2007/11/
               xmlns:v2=” http://schemas.microsoft.com/windows/2010/08/DeviceMetadata/PackageInfov2”>

  <MetadataKey>
      <HardwareIDList>
        <HardwareID>DOID:MBAE:0:L9@E}}DT2.*F65MQA57Y+L</HardwareID>
      </HardwareIDList>
      <Locale default="true">EN-US</Locale>
      <LastModifiedDate>2008-01-24T00:00:00Z</LastModifiedDate>
      <v2:MultipleLocale>true</v2:MultipleLocale>
  </MetadataKey>

  <PackageStructure>
      <Metadata MetadataID="http://schemas.microsoft.com/windows/DeviceMetadata/PackageInfo/2007/11">PackageInfo.xml</Metadata>
      <Metadata MetadataID="http://schemas.microsoft.com/windows/DeviceMetadata/ServiceInfo/2007/11/">ServiceInformation</Metadata>
      <Metadata MetadataID=”http://schemas.microsoft.com/windows/DeviceMetadata/WindowsInfo/2007/11/”>WindowsInformation</Metadata>
    </PackageStructure>
</PackageInfo>
```
