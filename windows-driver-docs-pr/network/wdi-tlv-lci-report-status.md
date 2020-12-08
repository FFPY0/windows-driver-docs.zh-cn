---
title: WDI_TLV_LCI_REPORT_STATUS
description: WDI_TLV_LCI_REPORT_STATUS 是一种 TLV，其中包含位置配置信息 (LCI) 报表的状态结果，如果在精确计时度量期间请求了某个位置，则 (INTERNAL.H) 请求。
ms.date: 02/15/2019
keywords:
- 从 Windows Vista 开始 WDI_TLV_LCI_REPORT_STATUS 网络驱动程序
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 15ad96c3a6945fa49082f58e0177b68ae069099b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820559"
---
# <a name="wdi_tlv_lci_report_status"></a>WDI_TLV_LCI_REPORT_STATUS

**WDI_TLV_LCI_REPORT_STATUS** 是一种 TLV，其中包含位置配置信息 (LCI) 报表的状态结果，如果在精确计时度量期间请求了某个位置，则 (internal.h) 请求。

此 TLV 用于 [WDI_TLV_FTM_RESPONSE](wdi-tlv-ftm-response.md)。

## <a name="tlv-type"></a>TLV 类型

0x15F

## <a name="length"></a>长度

UINT32) 的大小 (以字节为单位）。

## <a name="values"></a>值

| 类型 | 描述 |
| --- | --- |
| [**WDI_LCI_REPORT_STATUS**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_lci_report_status) | LCI 报表的状态。 |

## <a name="requirements"></a>要求

**支持的最低客户端**： windows 10 版本 1903 **支持的最低服务器**： Windows server 2016 **标头**： Wditypes. hpp
