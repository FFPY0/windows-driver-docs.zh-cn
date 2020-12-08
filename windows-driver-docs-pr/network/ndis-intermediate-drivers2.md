---
title: NDIS 中间驱动程序指南
description: NDIS 中间驱动程序指南
keywords:
- 中间驱动程序 WDK 网络
- 网络驱动程序 WDK，中间驱动程序
- NDIS WDK，中间驱动程序
- NDIS 中间驱动程序 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 648e62a59abbfbd2de0ae00c56ff56cef3c8e2eb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825065"
---
# <a name="ndis-intermediate-drivers-guide"></a>NDIS 中间驱动程序指南

顶层协议驱动程序和微型端口驱动程序之间的 NDIS 中间驱动程序接口。 可能需要中间驱动程序的一些应用程序包括：

-   旧传输驱动程序与管理传输驱动程序未知的媒体类型的微型端口驱动程序之间的媒体转换。

-   出于安全或其他目的进行数据筛选。

-   负载平衡故障转移 (LBFO) 解决方案。

-   监视和收集网络数据统计信息。

在尝试编写中间驱动程序之前，应阅读有关 NDIS 微型端口和协议驱动程序的信息。 有关 NDIS 微型端口驱动程序的详细信息，请参阅 [Ndis 微型端口驱动程序](roadmap-for-developing-ndis-miniport-drivers.md)。 有关 NDIS 协议驱动程序的详细信息，请参阅 [Ndis 协议驱动程序](./roadmap-for-developing-ndis-protocol-drivers.md)。

以下部分介绍了中间驱动程序，并说明了如何创建和安装此类驱动程序：

[NDIS 中间驱动程序的开发路线图](roadmap-for-developing-ndis-intermediate-drivers.md)

[NDIS 中间驱动程序简介](introduction-to-ndis-intermediate-drivers.md)

[编写 NDIS 中间驱动程序](writing-ndis-intermediate-drivers.md)

[中间驱动程序设计概念](intermediate-driver-design-concepts.md)

[安装中间驱动程序](installing-an-intermediate-driver.md)

 

