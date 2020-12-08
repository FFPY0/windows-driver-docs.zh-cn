---
title: HS_SIM_IDENTITY 结构
description: HS_SIM_IDENTITY 结构包含 EAP SIM 或 EAP 身份验证所需的 SIM 识别信息。
keywords:
- 从 Windows Vista 开始 HS_SIM_IDENTITY 结构网络驱动程序
- 从 Windows Vista 开始 PHS_SIM_IDENTITY 结构指针网络驱动程序
ms.date: 07/31/2017
ms.localizationpriority: medium
ms.openlocfilehash: 78ade44cbb16a11c4886127609eb27b74cb48eb3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823887"
---
# <a name="hs_sim_identity-structure"></a>HS \_ SIM \_ 标识结构

[!include[Wi-Fi Hotspot Offloading deprecation](../includes/wi-fi-hotspot-offloading-deprecation.md)]


**HS \_ sim \_ 标识** 结构包含 eap sim 或 eap 身份验证所需的 SIM 识别信息。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
typedef struct _HS_SIM_IDENTITY {
  eHS_SIM_TYPE SimType;
  DWORD        dwMNC;
  DWORD        dwMCC;
  DWORD        dwNID;
  DWORD        dwSID;
  DWORD        dwEapMethods;
} HS_SIM_IDENTITY, *PHS_SIM_IDENTITY;
```

<a name="members"></a>成员
-------

**SimType**  
SIM 的类型，无论是 GSM 还是 CDMA，都不是。 如果网络是 GSM，则会定义 **dwMNC** 和 **dwMCC** 字段对，而对于 CDMA，必须定义 **dwSID** 和 **dwNID** 字段对。

**dwMNC**  
如果 SIM 为 GSM 类型，则使用。

移动网络代码 (GSM 网络的 MNC) 。

**dwMCC**  
如果 SIM 为 GSM 类型，则使用。

移动国家/地区代码 (对 GSM 网络的 MCC) 。

**dwNID**  
如果 SIM 是 CDMA 类型，则使用。

CDMA 网络的网络标识号 (NID) 。

**dwSID**  
如果 SIM 是 CDMA 类型，则使用。

CDMA 网络的系统标识号 (SID) 。

**dwEapMethods**  
EAP 身份验证方法。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Hotspotoffloadplugin (包含 Hotspotoffloadplugin) </td>
</tr>
</tbody>
</table>

