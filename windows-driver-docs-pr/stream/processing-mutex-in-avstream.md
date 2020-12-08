---
title: 在 AVStream 中处理互斥
description: 在 AVStream 中处理互斥
keywords:
- AVStream mutex WDK
- mutex WDK AVStream
- 处理 mutex WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 542ca1486ff0785777d2f50acc489712bd671423
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790145"
---
# <a name="processing-mutex-in-avstream"></a>在 AVStream 中处理互斥





第三个 mutex 是处理互斥体。 单个筛选器和 pin 具有其自己的处理互斥体。 在筛选器和固定级别进行处理之前，AVStream 独立获取处理互斥体，以便同步对与处理相关的结构的访问。 AVStream 还会在其他操作期间获取处理互斥体，包括管道部分的绑定插针、睡眠或唤醒电源操作和更改描述符。 微型驱动程序可以手动获取互斥体来执行同步操作，如处理或描述符修改。 在进行处理时，微型驱动程序应获取处理互斥体，以使其不发生任何更改。

与其他两种类型的 mutex 一样，处理互斥体不会以递归方式获取。 这意味着，如果微型驱动程序尝试在处理时获取处理互斥体，则会发生死锁。

不要使用处理互斥体来在很长一段时间内挂起处理。 改为直接使用 **KSGATE * Xxx*** 函数操作处理控制入口。

已获取处理互斥体的线程以后不应尝试获取筛选器控件互斥体。

若要操作处理互斥体，请使用以下函数：

[**KsFilterAcquireProcessingMutex**](/windows-hardware/drivers/ddi/ks/nf-ks-ksfilteracquireprocessingmutex)、 [**KsPinAcquireProcessingMutex**](/windows-hardware/drivers/ddi/ks/nf-ks-kspinacquireprocessingmutex)、 [**KsFilterReleaseProcessingMutex**](/windows-hardware/drivers/ddi/ks/nf-ks-ksfilterreleaseprocessingmutex)、 [**KsPinReleaseProcessingMutex**](/windows-hardware/drivers/ddi/ks/nf-ks-kspinreleaseprocessingmutex)

 

