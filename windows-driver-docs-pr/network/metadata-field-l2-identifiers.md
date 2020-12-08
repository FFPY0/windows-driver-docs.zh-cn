---
title: 元数据字段 L2 标识符
description: 本部分介绍 Windows 筛选平台标注驱动程序的元数据字段 L2 标识符。
keywords:
- 元数据字段 L2 标识符网络驱动程序
ms.date: 11/09/2017
ms.localizationpriority: medium
ms.openlocfilehash: 18a0aa6399c3ca70794bafe1d4bf7a39121c5209
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803677"
---
# <a name="metadata-field-l2-identifiers"></a>元数据字段 L2 标识符

Windows 8 和 Windows Server 2012 引入了元数据字段 L2 标识符。

元数据字段 L2 标识符由位域表示。 这些标识符定义如下：

| 元数据字段标识符 | 描述 |
| --- | --- |
| FWPS_L2_METADATA_FIELD_ETHERNET_MAC_HEADER_SIZE | MAC 标头的大小（以字节为单位）。 |
| FWPS_L2_METADATA_FIELD_VSWITCH_DESTINATION_PORT_ID | 虚拟交换机上的目标端口的标识符。 |
| FWPS_L2_METADATA_FIELD_VSWITCH_PACKET_CONTEXT | 虚拟交换机数据包上下文的 **句柄** 。 |
| FWPS_L2_METADATA_FIELD_VSWITCH_SOURCE_NIC_INDEX | 虚拟交换机上源 NIC 的索引。 |
| FWPS_L2_METADATA_FIELD_VSWITCH_SOURCE_PORT_ID | 虚拟交换机上的源端口的标识符。 |
| FWPS_L2_METADATA_FIELD_WIFI_OPERATION_MODE | 当前本机802.11 操作模式。 |

## <a name="related-topics"></a>相关主题

[元数据字段标识符](metadata-field-identifiers.md)

[每个筛选层的元数据字段](metadata-fields-at-each-filtering-layer.md)

[FWPS_INCOMING_METADATA_VALUES0](/windows-hardware/drivers/ddi/fwpsk/ns-fwpsk-fwps_incoming_metadata_values0_)
