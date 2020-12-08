---
title: MSFC \_ FIBREPORTHBASTATISTICS WMI 类
description: MSFC \_ FIBREPORTHBASTATISTICS WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b0e009bd8797d620bc28fda108ace515f2ace4fe
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785557"
---
# <a name="msfc_fibreporthbastatistics-wmi-class"></a>MSFC \_ FIBREPORTHBASTATISTICS WMI 类


## <span id="ddk_msfc_fibreporthbastatistics_wmi_class_kr"></span><span id="DDK_MSFC_FIBREPORTHBASTATISTICS_WMI_CLASS_KR"></span>


WMI 客户端使用 MSFC \_ FibrePortHBAStatistics 类来查询 hba 微型端口驱动程序，以获取与 hba 上端口相关的统计信息。 MSFC \_ FibrePortHBAStatistics 类报告 [MSFC \_ HBAPortStatistics WMI 类](msfc-hbaportstatistics-wmi-class.md) 中的所有信息，以及端口的一些标识符信息。

MSFC \_ FibrePortHBAStatistics 类在 *Hbaapi* 中定义如下：

```cpp
class MSFC_FibrePortHBAStatistics
{
    [key] 
    string InstanceName;
    boolean Active;
    [
     Description ("Unique identifier for the port. "
                   "This identifier must be unique "
                   "among all ports on all adapters."
                   "The same value for the identifier "
                   "must be used for the same port "
                   "in other classes that expose port "
                   "information") : amended,
     WmiRefClass("MSFC_FibrePort"),
     WmiRefProperty("UniquePortId"),
     WmiDataId(1)
    ]
    uint64 UniquePortId;
    [WmiDataId(2),
     HBA_STATUS_QUALIFIERS
    ]
    uint32 HBAStatus;
    // Note 4 byte padding
    [ WmiDataId(3) ]
    MSFC_HBAPortStatistics Statistics;
};
```

由 WMI 工具套件编译时，此类定义生成以下数据结构：

[**MSFC \_ FibrePortHBAStatistics**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_msfc_fibreporthbastatistics)

没有与此 WMI 类相关联的方法。

 

