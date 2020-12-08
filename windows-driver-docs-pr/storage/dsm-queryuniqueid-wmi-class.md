---
title: DSM \_ QUERYUNIQUEID WMI 类
description: DSM \_ QUERYUNIQUEID WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 32e288518c1e6397fe5327b006d48447fc7688d9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835323"
---
# <a name="dsm_queryuniqueid-wmi-class"></a>DSM \_ QUERYUNIQUEID WMI 类


MPIO 发布 DSM \_ QUERYUNIQUEID WMI 类，但要求 DSM 注册 GUID 并处理其实现。 WMI 客户端使用 DSM \_ QUERYUNIQUEID WMI 类来查询路径的唯一标识符。

```cpp
class DSM_QueryUniqueId
{

    [key, read]
    string InstanceName;

    [read]
    boolean Active;

    //
    // This Identifier needs to be set by DSMs that want management applications
    // like VDS to be able to manage the devices controlled by the particular DSM.
    // This DsmUniqueId will be used in conjuction with the DsmPathId to construct
    // a path identitifer that is unique not just among all paths known to this DSM,
    // but also among all the DSMs present on the system.
    //
    [WmiDataId(1),
     DisplayName("DSM Unique Identifier") : amended,
     Description("DSM Unique Identifier to be used by a management application") : amended
    ]
    uint64 DsmUniqueId;
};
```

当 WMI 工具套件编译此类定义时，它将生成 [**DSM \_ QueryUniqueId**](/windows-hardware/drivers/ddi/mpiodisk/ns-mpiodisk-_dsm_queryuniqueid) 数据结构。 没有与此 WMI 类相关联的方法。

 

