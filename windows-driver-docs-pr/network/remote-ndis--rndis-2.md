---
title: 远程 NDIS (RNDIS) 简介
description: 远程 NDIS (RNDIS) 简介
keywords:
- 远程 NDIS WDK 网络
- 网络驱动程序 WDK，远程 NDIS
- RNDIS
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e2ae0735eb53f10e53a3412af4687589d17b8e7c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782139"
---
# <a name="introduction-to-remote-ndis-rndis"></a>远程 NDIS (RNDIS) 简介





远程 NDIS (RNDIS) 是一种与总线无关的类规范，适用于动态即插即用上的以太网 () PnP 总线（例如 USB、1394、蓝牙和自动限制）的以太网 () 802.3。 远程 NDIS 通过抽象控件和数据通道定义主机计算机和远程 NDIS 设备之间与总线无关的消息协议。 远程 NDIS 的精确度足以允许主机计算机上的远程 NDIS 设备具有与供应商无关的类驱动程序支持。

Windows XP 中的 Microsoft Windows 版本包括用于 USB 设备的远程 NDIS 驱动程序。 若要将此驱动程序与 USB 设备一起使用，IHV 必须提供遵循 [远程 NDIS INF 模板](remote-ndis-inf-template.md)中的模板的 INF 文件。

远程 NDIS 消息从主机发送到远程 NDIS 设备，远程 NDIS 设备使用适当的完成消息进行响应。 消息也将以未经请求的方式从远程 NDIS 设备发送到主机。

本节包括：

[远程 NDIS (RNDIS) 概述](overview-of-remote-ndis--rndis-.md)

[远程 NDIS 通信](remote-ndis-communication.md)

[远程 NDIS 到 USB 的映射](remote-ndis-to-usb-mapping.md)


 

 





