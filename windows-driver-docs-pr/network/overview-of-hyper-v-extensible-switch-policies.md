---
title: Hyper-V 可扩展交换机策略概述
description: Hyper-V 可扩展交换机策略概述
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ef92a710b8c05c08569dcf374f06ac4834b1857d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801379"
---
# <a name="overview-of-hyper-v-extensible-switch-policies"></a>Hyper-V 可扩展交换机策略概述


Hyper-v 平台和可扩展交换机接口提供一个基础结构，用于管理可扩展交换机的交换机和端口策略。 这些策略通过 PowerShell cmdlet 和基于 WMI 的应用程序进行管理。 此基础结构还支持策略的存储和迁移。

独立软件供应商 (Isv) 可以使用此基础结构来注册其自己的自定义策略。 注册后，可以通过内置的 Hyper-v 策略接口发现和管理这些策略。 可以在每个端口级别或按交换机级别配置策略的属性。

除了自定义策略属性以外，Hyper-v 可扩展交换机接口还提供基础结构，以根据每个端口或每个交换机获取自定义策略属性的状态信息。 此状态信息称为 *功能状态* 信息。

可扩展交换机自定义策略数据通过使用托管对象格式 (MOF) 类定义注册到 WMI 管理层。 下面显示了一个用于自定义端口策略属性的 MOF 类的示例。

```C++
#pragma namespace("\\\\.\\root\\virtualization\\v2")

[ Dynamic, 
 UUID("F2F73F23-2B8E-457a-96C4-F541201C9150"),
 ExtensionId("5CBF81BE-5055-47CD-9055-A76B2B4E369E"), 
 Provider("VmmsWmiInstanceAndMethodProvider"), 
 Locale(0x409),
 InterfaceVersion("1"),
 InterfaceRevision("0"),
DisplayName("VendorName Port Settings Friendly Name") : Amended,
Description("VendorName Port Settings detailed description.") : Amended]
class Vendor_SampleFeatureSettingData: Msvm_EthernetSwitchPortFeatureSettingDataMsvm
{
  [WmiDataId(1),
   InterfaceVersion("1"),
   InterfaceRevision("0")]
  uint8  IntValue8 = 0;

  [WmiDataId(2),
   InterfaceVersion("1"),
   InterfaceRevision("0")]
  uint16 IntValue16 = 0;

  [WmiDataId(3),
   InterfaceVersion("1"),
   InterfaceRevision("0")]
  uint32 IntValue32 = 0;

  [WmiDataId(4),
   InterfaceVersion("1"),
   InterfaceRevision("0")]
  uint64 IntValue64 = 0;

  [WmiDataId(5),
   InterfaceVersion("1"),
   InterfaceRevision("0"), 
   MaxLen(255)]
  string FixedLengthString = "";

  [WmiDataId(6),
   InterfaceVersion("1"),
   InterfaceRevision("0")]
  string VariableLengthString = "";

  [WmiDataId(7),
   InterfaceVersion("1"),
   InterfaceRevision("0"),
   Max(8)]
  uint32 FixedLengthArray[] = {};

  [WmiDataId(8),
   InterfaceVersion("1"),
   InterfaceRevision("0")]
  uint32 VariableLengthArray[] = {};

};
```

当 MOF 数据传输到基础可扩展交换机扩展时，WMI 管理层会序列化这些数据。 MOF 类序列化为可由 Hyper-v 可扩展交换机扩展处理的相应 C 结构。 下面显示了从上一个示例中为 MOF 类序列化的 C 结构的示例。

```C++
#pragma pack(8)

typedef struct _VARIABLE_LENGTH_ARRAY
{
    UINT32 Buffer[1];
} VARIABLE_LENGTH_ARRAY;

typedef struct _SAMPLE_FEATURE_SETTINGS
{
    UINT8  IntValue8;
    UINT32 IntValue16;
    UINT32 IntValue32;
    UINT64 IntValue64;
    UINT16 FixedLengthStringByteCount;
    WCHAR  FixedLengthString[256]; 
    UINT32 VariableLengthStringOffset;    // offset to VARIABLE_LENGTH_STRING structure
    UINT32 FixedLengthArrayElementCount;
    UINT32 FixedLengthArray[8];
    UINT32 VariableLengthArrayElementCount;
    UINT32 VariableLengthArrayOffset;   // offset to VARIABLE_LENGTH_ARRAY
} SAMPLE_FEATURE_SETTINGS;
 
typedef struct _VARIABLE_LENGTH_STRING
{
    USHORT StringLength;
    WCHAR  StringBuffer[1];
} VARIABLE_LENGTH_STRING;
```

此示例突出显示了 MOF 类序列化为可扩展交换机策略属性的相应 C 结构时出现的以下几点：

-   MOF 文件中的版本定义将转换为 USHORT 值，其中，高序位包含主要版本，低序位包含次版本。 版本是使用以下代码序列化的：

    `  (((MajorVersion) << 8) + (MinorVersion))`

    例如，上面 ) 的版本 ( "1" 将被序列化为0x0100 到的值 `(((1) << 8) + (0))` 。 版本 ( "1.1" ) 将被序列化为0x0101 到的值 `(((1) << 8) + (1))` 。

    将自定义策略属性颁发给基础扩展时，定义策略属性的结构的 **PropertyVersion** 成员包含序列化的版本值。

    例如，当可扩展交换机接口发出对象标识符 (OID) 请求 [oid \_ 交换机 \_ 端口 \_ 属性 \_ 添加](./oid-switch-port-property-add.md)时，oid 与 [**NDIS \_ 交换机 \_ 端口 \_ 属性 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_switch_port_property_parameters) 结构关联。 该结构的 **PropertyVersion** 成员包含序列化的版本值。

-   所有可变长度字符串都序列化为包含序列化 C 结构的缓冲区内的偏移量。 每个可变长度字符串的格式为此缓冲区偏移内的 **可变 \_ 长度 \_ 字符串** 结构。

 

