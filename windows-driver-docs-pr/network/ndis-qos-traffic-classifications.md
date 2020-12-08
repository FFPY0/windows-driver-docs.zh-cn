---
title: NDIS QoS 流量分类
description: NDIS QoS 流量分类
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fabc0dfb54e6f1aacd26b540ac603e7ceb8ea73a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801543"
---
# <a name="ndis-qos-traffic-classifications"></a>NDIS QoS 流量分类


NDIS 服务质量 (QoS) 为网络适配器按优先级排列的传递来分类传输（或 *传出* 数据包）。 每个流量分类均指定以下各项：

-   基于出口数据包数据中的数据模式的分类 *条件* 。

    从 NDIS 6.30 开始，分类条件基于16位值，如 UDP 或 TCP 目标端口，或者 (MAC) EtherType 的媒体访问控制。

-   定义要用于处理传出数据包的流量类的分类 *操作* 。

    从 NDIS 6.30 开始，分类操作指定 802.1 p 优先级别。

**注意**  流量分类也称为 IEEE 802.1 规范中的 "应用程序优先级"。

 

NDIS QoS 流量分类适用于以下类型的出口数据包流量：

-   基于卸载到微型端口驱动程序的流量（例如光纤通道 over 以太网 (FCoE) 或 iSCSI 数据包）的数据包。

-   基于由微型端口驱动程序管理和强制实施的连接的数据包，如 RDMA。

因为 NDIS QoS 流量分类不适用于操作系统生成的 TCP/IP 流量，所以微型端口驱动程序无需执行数据包检查。 相反，如果分类条件与驱动程序已卸载或管理的数据包类型匹配，则只需将分类操作应用到属于该类型的所有包。 例如，如果为 FCoE 的卸载启用了微型端口驱动程序，并且分类条件指定了 iSCSI TCP 端口号 (860 或 3260) ，则驱动程序将优先级别为分类操作定义的所有出口 iSCSI 数据包的优先级。

 ( # A0) 的 DCB 组件通过 oid [ \_ QOS \_ 参数](./oid-qos-parameters.md)的 oid 方法请求来指定流量分类。 此 OID 请求包含一个 [**ndis \_ qos \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_parameters) 结构，该结构指定一个 [**ndis \_ qos \_ 分类 \_ 元素**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_classification_element) 结构的数组。 其中每个结构都定义了一个流量分类。

DCB 组件指定将应用于所有与其他分类条件不匹配的传出数据包的 *默认* 流量分类。 在这种情况下，网络适配器将与默认分类关联的 IEEE 802.1 p 优先级分配给这些出口数据包。 默认流量分类具有以下属性：

-   它具有 "NDIS \_ QOS 条件默认类型" 的流量分类条件 \_ \_ 。

-   它是在 [**NDIS \_ QOS \_ 分类 \_ 元素**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_qos_classification_element) 结构的数组中定义的第一个流量分类。

有关 DCB 组件的详细信息，请参阅 [用于数据中心桥接的 NDIS QoS 体系结构](ndis-qos-architecture-for-data-center-bridging.md)。

 

