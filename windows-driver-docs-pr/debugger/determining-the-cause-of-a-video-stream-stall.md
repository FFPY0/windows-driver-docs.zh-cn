---
title: 确定视频流停滞的原因
description: 确定视频流停滞的原因
keywords:
- 内核流调试，视频流停止，原因
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e4e04a4ed59a66fbb7156210326c6b849aaf1a9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96833669"
---
# <a name="determining-the-cause-of-a-video-stream-stall"></a>确定视频流停滞的原因


视频流延迟有两个基本原因：

-   **挂起。** 驱动程序未释放用户模式线程或内核模式线程。

-   **隔间。** 这是流路径中组件出现问题的结果。 一些可能的原因包括：
    -   捕获驱动程序未完成包。 在这种情况下，驱动程序组件或硬件可能是卡住的源。
    -   捕获驱动程序没有要完成的数据包。 在这种情况下，缓冲区可能会在编解码器或其他下游组件中停止。

如果可以再现该问题，请在此时附加调试器，以确定哪个是实际原因。

**确定问题是否是挂起的**

1.  将用户模式调试器附加到应用程序，并查找被阻止的用户模式线程。

2.  确定应用程序是否响应。 是否可以暂停图形？ 是否可以停止图形？ 如果停止并重新启动了图形，是否会重新启动流式处理？

3.  如果应用程序未响应，则尝试使用任务管理器来结束任务。 如果此操作失败，则会出现内核模式挂起。

**确定问题是否是一个延迟**

1.  确定示例在图形中的位置。 这可以在本地或在内核模式调试会话中完成。

2.  确定样本是否流动下游。 如果可以在 [GraphEdit](/windows/win32/directshow/simulating-graph-building-with-graphedit)中再现 bug，请在关系图中放置一个中间筛选器以显示示例。

3.  确定是否正在调用处理例程。 为此，可以在此例程中附加一个内核模式调试器并设置断点。

 

