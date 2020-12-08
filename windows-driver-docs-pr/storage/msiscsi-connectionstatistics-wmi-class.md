---
title: MSiSCSI \_ CONNECTIONSTATISTICS WMI 类
description: MSiSCSI \_ CONNECTIONSTATISTICS WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 34e8d60eb4b7c53f043f0d6e238a30f067806cee
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811431"
---
# <a name="msiscsi_connectionstatistics-wmi-class"></a>MSiSCSI \_ CONNECTIONSTATISTICS WMI 类


## <span id="ddk_msiscsi_connectionstatistics_wmi_class_kr"></span><span id="DDK_MSISCSI_CONNECTIONSTATISTICS_WMI_CLASS_KR"></span>


MSiSCSI \_ CONNECTIONSTATISTICS WMI 类公开连接统计信息。 此类在 Iscsiprf 中定义为如下。

```cpp
class MSiSCSI_ConnectionStatistics : Win32_PerfRawData {
  [read,key] String  InstanceName;
  [read] boolean  Active;
  [read, WmiDataId(1), WmiVersion(1), 
    cpp_quote(
    "\n    //Text-based identifier for this Initiator that 
    is globally unique.\n"
    "    //The Initiator Name is independent of the location 
    of the initiator.\n"),
    MaxLen(MAX_ISCSI_NAME_LEN)] 
    string  iSCSIName;
  [read, WmiDataId(2), WmiVersion(1), Description("The iSCSI 
    connection ID for this connection instance."): amended] 
    uint16  CID; //session wide namespace
  [read, WmiDataId(3), Description("A uniquely generated 
    session ID used only internally.  Do not mix this with 
    ISID or SSID"): amended,
    cpp_quote(
    "\n    //A uniquely generated session ID used only 
    internally.  Do not mix this with ISID or SSID\n"),
    WmiVersion(1)] 
    uint64  USID;
  [WmiDataId(4), DisplayName("Adapter Id") : amended, 
    DisplayInHex, description("Id that is globally unique to 
    each instance of each adapter. Using the address of the 
    Adapter Extension is a good idea.") : amended]
    uint64  UniqueAdapterId;
  [WmiDataId(5), DisplayName("Bytes Sent"): amended, 
    PerfDefault, CounterType(0x10410400),
    //    32bit per sec display
    DefaultScale(0), PerfDetail(100), read, 
    Description("Count of # of bytes sent over this 
    connection"): amended] 
    uint64  BytesSent;
  [WmiDataId(6), DisplayName("Bytes Received"): amended, 
    PerfDefault, CounterType(0x10410400),
    //    32bit per sec display
    DefaultScale(0), PerfDetail(100), read, 
    Description("Count of # of bytes received over this 
    connection"): amended] 
    uint64  BytesReceived;
  [WmiDataId(7), DisplayName("PDUs Sent"): amended, 
    PerfDefault, CounterType(0x10410400),
    //    32bit per sec display
    DefaultScale(0), PerfDetail(100), read, 
    Description("Count of # of  PDU Commands Sent over this 
    connection"): amended] 
    uint64  PDUCommandsSent;
  [WmiDataId(8), DisplayName("PDUs Received"): amended, 
    PerfDefault, CounterType(0x10410400),
    //    32bit per sec display
    DefaultScale(0), PerfDetail(100), read, 
    Description("Count of # of PDUResponses received over 
    this connection"): amended] 
    uint64  PDUResponsesReceived;
};
```

当 WMI 工具套件编译上述类定义时，它会生成 [**MSiSCSI \_ ConnectionStatistics**](/windows-hardware/drivers/ddi/iscsiprf/ns-iscsiprf-_msiscsi_connectionstatistics) 数据结构。

发起程序必须向 \_ 以下目标实例名称注册 MSiSCSI CONNECTIONSTATISTICS WMI 类：

```cpp
targetname_#:#
```

第一个数字符号 (\#) 是 [**MSiSCSI \_ ConnectionStatistics**](/windows-hardware/drivers/ddi/iscsiprf/ns-iscsiprf-_msiscsi_connectionstatistics)结构的 **USID** 成员中的值，第二个数字符号 (\#) 是此类的 **CID** 成员中的值。

 

