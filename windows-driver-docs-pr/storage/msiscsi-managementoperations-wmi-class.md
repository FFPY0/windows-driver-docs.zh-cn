---
title: MSiSCSI \_ MANAGEMENTOPERATIONS WMI 类
description: MSiSCSI \_ MANAGEMENTOPERATIONS WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 0db38deff927fb7b38cb354b3453a08c24b92bd2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827445"
---
# <a name="msiscsi_managementoperations-wmi-class"></a>MSiSCSI \_ MANAGEMENTOPERATIONS WMI 类


MSiSCSI \_ MANGEMENTOPERATIONS WMI 类包含用于对目标地址执行 ICMP ping 请求的 ping 方法。 此类在管理 mof 中定义为：

```cpp
class MSiSCSI_ManagementOperations
{
    //
    // This class must be registered using PDO instance names
    //
    [key]
    string InstanceName;
 
    boolean Active;

    [WmiMethodId(10),
     Implemented,
     Description("Perform an ICMP ping") : amended,
     cpp_quote(
"//\n"
"// This method is recommended.\n"
"//\n"             
"// Ping will perform ICMP ping requests to the destination address \n"
"// and return the number of ping responses received. This is only supported\n"
"// by some HBA, use the ping command for the software initiator.\n"
"//\n"
              )            
    ]
    void PingIPAddress(
                     [in,
                      Description("Number of requests to send") : amended
                     ] uint32 RequestCount,

                     [in,
                      Description("Number of bytes in each request") : amended
                     ] uint32 RequestSize,

                     [in,
                      Description("Number of ms to wait for response") : amended
                     ] uint32 Timeout,

                     [in,
                      description("IP address to ping") : amended
                     ] ISCSI_IP_Address Address,
 
                     [out,
                      ISCSI_STATUS_QUALIFIERS
                     ] ISCSI_STATUS Status,
 
                     [out,
                      Description("Number of responses received") : amended
                     ] uint32 ResponsesReceived

                    );

 
};
```

当 WMI 工具套件编译上述类定义时，它会生成一个 [MSiSCSI \_ ManagementOperations](/windows-hardware/drivers/ddi/index) 数据结构。

 

