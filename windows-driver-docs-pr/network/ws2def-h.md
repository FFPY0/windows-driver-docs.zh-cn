---
title: Ws2def.h
description: 本部分包含 Ws2def 标头的内核模式网络驱动程序主题。
keywords:
- Ws2def 网络驱动程序
ms.date: 08/08/2017
ms.localizationpriority: medium
ms.openlocfilehash: d1b99e0467712e365d79b230117e14d753ad8b66
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813627"
---
# <a name="ws2defh"></a>Ws2def.h

本部分包含 Ws2def 标头的内核模式网络驱动程序主题。 此标头包含在 Windows SDK 中，因为它也与用户模式网络应用程序共享。

Ws2def 标头包含 Winsock2 规范的定义。 它包含在 Winsock2. h 中。 用户模式应用程序应包括 Winsock2 .h，而不是直接包含 Ws2def。 Ws2def 也不能包含在包含 Winsock .h 的模块中。

> [!IMPORTANT]
> 本部分的主题包含以下内容的页面：定义、宏、Oid、状态指示和其他不属于网络驱动程序引用 (结构、枚举、函数和回调) 的数据结构。 
>
> 有关此标头的网络驱动程序参考的详细信息，请参阅 [Ws2def (reference) ](/previous-versions/windows/hardware/drivers/mt808757(v=vs.85))。

## <a name="in-this-section"></a>在本节中

* [AF_INET](af-inet.md)
* [AF_INET6](af-inet6.md)
* [SIO_ADDRESS_LIST_CHANGE](sio-address-list-change.md)
* [SIO_ADDRESS_LIST_QUERY](sio-address-list-query.md)
* [SO_BROADCAST](so-broadcast.md)
* [SO_CONDITIONAL_ACCEPT](so-conditional-accept.md)
* [SO_EXCLUSIVEADDRUSE](so-exclusiveaddruse.md)
* [SO_KEEPALIVE](so-keepalive.md)
* [SO_RCVBUF](so-rcvbuf.md)
* [SO_REUSEADDR](so-reuseaddr.md)
