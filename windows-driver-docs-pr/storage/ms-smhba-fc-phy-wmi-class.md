---
title: MS \_ SMHBA \_ FC \_ PHY WMI 类
description: MS \_ SMHBA \_ FC \_ PHY WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 1603fb64e8ab4287fc6c4f24acc5f943f7a36eaa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834995"
---
# <a name="ms_smhba_fc_phy-wmi-class"></a>MS \_ SMHBA \_ FC \_ PHY WMI 类


支持存储管理 API 的 HBA 微型端口驱动程序使用 MS \_ SMHBA \_ FC \_ PHY 类公开关联 FC 端口的物理属性。 每个端口都应有此类的一个实例。

\_ \_ 在 Hbaapi 中，MS SMHBA FC \_ PHY 类定义如下 *Hbaapi.mof*：

```cpp
class MS_SMHBA_FC_PHY 
{
    [WmiDataId(1), HBAType("HBA_FCPHYSPEED")]
    uint32  PhySupportSpeed;

    [WmiDataId(2), HBAType("HBA_FCPHYSPEED")]
    uint32  PhySpeed;      

    [WmiDataId(3), HBAType("HBA_FCPHYTYPE")]
    uint8   PhyType;

    [WmiDataId(4)]
    uint32  MaxFrameSize; 
};
```

当 WMI 工具套件编译此类定义时，它将生成以下数据结构：

[**MS \_ SMHBA \_ FC \_ PHY**](/windows-hardware/drivers/ddi/hbapiwmi/ns-hbapiwmi-_ms_smhba_fc_phy)

没有与此 WMI 类相关联的方法。

 

