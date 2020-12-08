---
title: ISCSI \_ SESSIONSTATICINFO WMI 类
description: ISCSI \_ SESSIONSTATICINFO WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d67610fcd31941f7a4ae686e0c71971ade1280ad
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835093"
---
# <a name="iscsi_sessionstaticinfo-wmi-class"></a>ISCSI \_ SESSIONSTATICINFO WMI 类


## <span id="ddk_iscsi_sessionstaticinfo_wmi_class_kr"></span><span id="DDK_ISCSI_SESSIONSTATICINFO_WMI_CLASS_KR"></span>


ISCSI \_ SessionStaticInfo 类用于存储会话的静态特性。 此类在 *管理 mof* 中定义为：

```cpp
class ISCSI_SessionStaticInfo {
  [read, WmiDataId(1), Description("A uniquely generated
    session ID used only internally.  Do not confuse this
    with ISID or SSID"): amended, WmiVersion(1)] 
    uint64  UniqueSessionId;
  [read, WmiDataId(2), WmiVersion(1), 
    cpp_quote(
    "\n  //Text-based identifier for this Initiator that
    is globally unique.\n"
    "    //The Initiator Name is independent of the location
    of the initiator.\n"),
    MaxLen(MAX_ISCSI_NAME_LEN)] string InitiatoriSCSIName;
  [read, WmiDataId(3), WmiVersion(1), Description("Name of
    the target"): amended, MaxLen(MAX_ISCSI_NAME_LEN)] 
    String  TargetiSCSIName;
  [read, WmiDataId(4), Description("Target-defined portion
    of the iSCSI Session ID"): amended, WmiVersion(1)] 
    uint16  TSID;
  [read, WmiDataId(5), Description("Initiator-defined
    portion of the iSCSI Session ID"): amended,
    WmiVersion(1)] 
    uint8  ISID[6];
  [read, WmiDataId(6), 
    cpp_quote(
    "\n  // If set to true, indicates that the initiator
    must wait for an R2T before  \n"
    "    // sending data to the target.  If false, the
    initiator may send data immediately, within
    limits\n"
    "    // set by FirstBurstSize and the expected data
    transfer length of the request.\n"),WmiVersion(1)] 
    boolean  InitialR2t;
  [read, WmiDataId(7), 
    cpp_quote(
    "\n  // Indicates whether the initiator and target
    have agreed to support \n"
    "    // immediate commands on this session\n"),
    WmiVersion(1)] 
    boolean  ImmediateData;
  [read, WmiDataId(8), ISCSI_SESSION_TYPE_QUALIFIERS,
    cpp_quote("\n"
    " // Type of iSCSI session\n"
    " // normalSession - session is a normal iSCSI
    session\n"
    " // bootSession   - session is being used to boot
    an initiator\n"
    " // discoverySession -session is being used only for
    discovery\n"
    " // copySession   - session is being used by a
    copy manager\n"
    "\n"), WmiVersion(1)] 
    ISCSI_SESSION_TYPE  Type;
  [read, WmiDataId(9),
    ISCSI_HEADER_INTEGRITY_TYPE_QUALIFIERS,
    cpp_quote(
    "\n  // The name of the iSCSI header digest scheme in
    use within this session.\n"),
    WmiVersion(1), MaxLen(255)] 
    ISCSI_HEADER_INTEGRITY_TYPE  HeaderIntegrity;
  [read, WmiDataId(10),
    ISCSI_DATA_INTEGRITY_TYPE_QUALIFIERS,
    cpp_quote(
    "\n  // The name of the iSCSI data digest scheme in
    use within this session.\n"),
    WmiVersion(1), MaxLen(255)] 
    ISCSI_DATA_INTEGRITY_TYPE  DataIntegrity;
  [read, WmiDataId(11),
    cpp_quote(
    "\n  // False indicates that data PDU Sequences may\n"
    "    // be transferred in any order.  True indicates
    that data PDU \n"
    "    // Sequences must be transferred using continuously
    increasing offsets,\n"
    "    // except during error recovery.\n"),
    WmiVersion(1)] 
    boolean  DataSequenceInOrder;
  [read, WmiDataId(12), 
    cpp_quote(
    "\n  // False indicates that data PDUs within
    Sequences may be in any order.\n"
    "    // True indicates that data PDUs within sequences
    must be at continuously\n"
    "    // increasing addresses, with no gaps or overlay
    between PDUs.\n"), WmiVersion(1)] 
    boolean  DataPduInOrder;
  [read, WmiDataId(13),
    cpp_quote(
    "\n  // The level of error recovery negotiated between
    the initiator and the target. Higher numbers\n"
    "    // represent more detailed recovery schemes.\n"),
    WmiVersion(1)] 
    uint8  ErrorRecoveryLevel;
  [read, WmiDataId(14), 
    cpp_quote(
    "\n  // The maximum number of outstanding request-to
    -transmit (R2T) \n"
    "    // per task within this session\n"),WmiVersion(1)] 
    uint32  MaxOutstandingR2t;
  [read, WmiDataId(15), 
    cpp_quote(
    "\n  // The maximum data payload size supported for
    command \n"
    "    // or data PDUs within this session.\n"),
    WmiVersion(1)] 
    uint32  MaxRecvDataSegmentLength;
  [read, WmiDataId(16), 
    cpp_quote("\n  // The maximum length supported for
    unsolicited data  \n"
    "  // sent within this session.\n"), WmiVersion(1)] 
    uint32  FirstBurstLength;
  [read, WmiDataId(17), 
    cpp_quote(
    "\n  // The maximum number of bytes which can be sent
    within a \n"
    "    // single sequence of Data-In or Data-Out
    PDUs.\n"), WmiVersion(1)] 
    uint32  MaxBurstLength;
  [read, WmiDataId(18), ISCSI_AUTH_TYPES_QUALIFIERS] 
    ISCSI_AUTH_TYPES  AuthType;
  [read, WmiDataId(19), 
    cpp_quote(
    "\n  // The time, in seconds, for which the target will 
    keep connection and session state for possible,\n"
    "    // recovery after a connection termination or
    reset.\n"), WmiVersion(1)] 
    uint32  LogoutLoginMaxTime;
  [read, WmiDataId(20), 
    cpp_quote(
    "\n  // The maximum number of connections that 
    will be \n"
    "    // allowed within this session \n"), WmiVersion(1)] 
    uint32  MaxConnections;
  [read, WmiDataId(21), 
    cpp_quote(
    "\n  // The number of TCP connections that currently
    belong to this session  \n"), WmiVersion(1)] 
    uint16  ConnectionCount;
  [WmiDataId(22), read, DisplayName("List of Connections") :
    amended, Description("Variable length array of
    ISCSI_ConnectionStaticInfo.  ConnectionCount specifies
    the number of elements in the array") : amended,
    WmiSizeIs("ConnectionCount")]  
    ISCSI_ConnectionStaticInfo  ConnectionsList[];
};
```

当 WMI 工具套件编译上述类定义时，它将生成 [**ISCSI \_ SessionStaticInfo**](/windows-hardware/drivers/ddi/iscsimgt/ns-iscsimgt-_iscsi_sessionstaticinfo) 数据结构。

 

