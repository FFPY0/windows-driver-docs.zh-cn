---
title: Storport 中的多层重置
description: Storport 中的多层重置
keywords:
- Storport 驱动程序 WDK，错误
- 错误 WDK Storport
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e5696bf4aba92099aac7c96374bad00a47f84a81
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804419"
---
# <a name="multi-tier-reset-in-storport"></a>Storport 中的多层重置


## <span id="ddk_multi_tier_reset_in_storport_kg"></span><span id="DDK_MULTI_TIER_RESET_IN_STORPORT_KG"></span>


Storport 驱动程序实现更高级的重置方案，而不是 SCSI 端口驱动程序。 重置整个总线的 SCSI 端口方法是一项成本高昂的操作，即使在 SCSI 总线上也是如此。 在高性能的总线（如光纤通道总线）上，可能无法进行总线重置。

如果可能，Storport 驱动程序和相关的更高级别驱动程序将尝试重置逻辑单元。 如果此操作失败，Storport 将尝试重置设备。 最后，如果此方法也失败，则 Storport 将重置总线。 此序列生成的总线重置操作明显减少。

为了满足高性能总线的更复杂要求，Storport 实现了一种多层重置操作，该操作允许更多的重置选项。 可以通过 SRBs （而不是一个）发送两种类型的重置：

最后，通过同步回调例程 [**HwStorResetBus**](/windows-hardware/drivers/ddi/storport/nc-storport-hw_reset_bus)来影响总线重置操作。

 

