---
title: 数据日志记录
description: 数据日志记录
ms.assetid: 1e4f00e0-0fc6-459d-bbdd-02fbca5b9945
keywords:
- 对标注 WDK Windows 筛选平台，日志记录的数据进行分类
- 日志记录 WDK Windows 筛选平台
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b953b68419a12757178d6c3d73d524e4132da131
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562275"
---
# <a name="data-logging"></a>数据日志记录


若要确定数据应该是记录，一个标注[classifyFn](https://msdn.microsoft.com/library/windows/hardware/ff544887)标注函数可以检查数据字段、 元数据字段和任何传递给它的原始数据的任意组合以及已存储的任何相关数据与筛选器或数据相关联的上下文中流。

例如，如果跟踪网络层筛选器将放弃多少传入 （入站） 的 IPv4 数据包的标注，则标注添加到筛选器引擎在 FWPM\_层\_入站\_IPPACKET\_V4\_放弃层。 在此情况下，标注的[classifyFn](https://msdn.microsoft.com/library/windows/hardware/ff544887)标注函数可能类似于下面的示例：

```C++
ULONG TotalDiscardCount = 0;
ULONG FilterDiscardCount = 0;

// classifyFn callout function
VOID NTAPI
 ClassifyFn(
    IN const FWPS_INCOMING_VALUES0  *inFixedValues,
    IN const FWPS_INCOMING_METADATA_VALUES0  *inMetaValues,
    IN OUT VOID  *layerData,
    IN const FWPS_FILTER0  *filter,
    IN UINT64  flowContext,
    IN OUT FWPS_CLASSIFY_OUT  *classifyOut
    )
{
  // Increment the total count of discarded packets
 InterlockedIncrement(&TotalDiscardCount);


  // Check whether a discard reason metadata field is present
 if (FWPS_IS_METADATA_FIELD_PRESENT(
 inMetaValues,
        FWPS_METADATA_FIELD_DISCARD_REASON))
  {
    // Check whether it is a general discard reason
 if (inMetaValues->discardMetadata.discardModule ==
        FWPS_DISCARD_MODULE_GENERAL)
    {
      // Check whether discarded by a filter
 if (inMetaValues->discardMetadata.discardReason ==
          FWPS_DISCARD_FIREWALL_POLICY)
      {
        // Increment the count of packets discarded by a filter
 InterlockedIncrement(&FilterDiscardCount);
      }
    }
  }

  // Take no action on the data
 classifyOut->actionType = FWP_ACTION_CONTINUE;
}
```

## <a name="related-topics"></a>相关主题


[classifyFn](https://msdn.microsoft.com/library/windows/hardware/ff544887)

 

 





