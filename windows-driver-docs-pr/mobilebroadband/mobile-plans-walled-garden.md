---
title: 移动计划围墙花园
description: 移动计划围墙花园
keywords:
- Windows Mobile 计划 mobile operators 围墙园
ms.date: 07/31/2019
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: b185c1594fa8ba1e77131b8fe05d1c7cf59a4807
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96805309"
---
# <a name="mobile-plans-walled-garden"></a>移动计划围墙花园

移动计划 *围墙园* 是在客户用完了数据时支持客户的关键所在。 即使没有备用 internet 连接（如 Wi-fi），也可以通过它访问 MO 直接门户。 这将使使用者能够购买其他数据计划并管理其订阅。

> [!NOTE]
> 移动计划体系结构不支持围墙园终结点的 IP 范围。 主机名必须用于 allowlisting。

MO Direct web 门户和 `GetBalance` API 终结点也必须属于此围墙园。

## <a name="walled-garden-endpoints"></a>围墙园终结点

只有少量的必需终结点对于最终用户始终是可访问的。 下表定义了围墙园所需的终结点。

| URL | HTTP/HTTPS |
| --- | --- |
| 数据市场 <span></span> 。 | https |
| 预览版 <span></span> . 数据市场 | https |
| windows live <span></span> .net | https |
| ctldl <span></span> . windowsupdate.log | http |
| cdp1-信任 <span></span> .com | http |
| <span></span>omniroot | http |
| vassg142 <span></span> omniroot | http |
| vassg142 <span></span> . omniroot | http |
| mscrl <span></span> | http |
| .crl <span></span> | http |
| <span></span>msftconnecttest | http |
| crl3 <span></span> . digicert | http |
| <span></span>Digicert | http |
| login <span></span> .com | http + https |
| storagetos <span></span> . 数据市场 | http + https |
| 数据市场 <span></span> 。 | http + https |
| 数据市场（mps） <span></span> | http + https |
| 暂存数据市场 <span></span> | http + https |
| mps-暂存数据市场 <span></span> | http + https |
