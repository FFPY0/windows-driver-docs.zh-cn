---
title: OID_CO_ADD_PVC
description: 本主题介绍) OID_CO_ADD_PVC 对象标识符 (OID。
keywords:
- OID_CO_ADD_PVC
ms.date: 11/03/2017
ms.localizationpriority: medium
ms.openlocfilehash: da24bc840336794f162dbfcdd52138f060857ba4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840005"
---
# <a name="oid_co_add_pvc"></a>OID_CO_ADD_PVC

OID_CO_ADD_PVC OID 由客户端发送到呼叫管理器，以将 (PVC) 永久虚拟连接添加到已配置的 Pvc 的 "呼叫管理器" 列表中。 PVC 的格式为 CO_PVC 结构，定义如下：

```c++
typedef struct _CO_PVC {
    NDIS_HANDLE             NdisAfHandle;
    CO_SPECIFIC_PARAMETERS  PvcParameters;
} CO_PVC, *PCO_PVC;
```

此结构的成员包含以下信息：

**NdisAfHandle**  
指定由 [NdisClOpenAddressFamilyEx](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndisclopenaddressfamilyex)返回的 NDIS 提供的句柄。

**PvcParameters**  
格式 [CO_SPECIFIC_PARAMETERS](/previous-versions/windows/hardware/network/ff545396(v=vs.85)) 的结构。 此结构包含用于描述 PVC 的特定于协议的参数。

PVC 由管理员手动配置。 监视此类活动的客户端通过将此 OID 发送到呼叫管理器通知新配置的 PVC 的呼叫管理器。 然后，其他客户端可以使用新配置的 PVC。

## <a name="requirements"></a>要求

**版本**： Windows Vista 和更高版本的 **标头**： Ntddndis (包括 Ndis .h) 
