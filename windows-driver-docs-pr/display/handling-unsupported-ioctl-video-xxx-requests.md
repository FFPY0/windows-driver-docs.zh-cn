---
title: 处理不受支持的 IOCTL_VIDEO_XXX 请求
description: 处理不受支持的 IOCTL_VIDEO_XXX 请求
keywords:
- 视频微型端口驱动程序 WDK Windows 2000，处理请求
- 请求处理 WDK 视频微型端口
- 不受支持的 IOCTL_VIDEO_XXX 请求 WDK 视频微型端口
- IOCTL_VIDEO_XXX 请求 WDK 视频微型端口
- I/o WDK 视频微型端口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2782fd28d66dcdc4985751d042b3bccd2b90122a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830669"
---
# <a name="handling-unsupported-ioctl_video_xxx-requests"></a>处理不受支持的 IOCTL \_ 视频 \_ XXX 请求


## <span id="ddk_handling_unsupported_ioctl_video_xxx_requests_gg"></span><span id="DDK_HANDLING_UNSUPPORTED_IOCTL_VIDEO_XXX_REQUESTS_GG"></span>


每个 [*HwVidStartIO*](/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_start_io)函数还必须处理对不受支持的 IOCTL \_ 视频 XXX 的接收 \_ *XXX*，如下所示：

1.  将输入 VRP 的 " **状态** " 字段设置为 "ERROR \_ 无效 \_ 函数"。

2.  将输入 VRP 的 **信息** 字段设置为零。

3.  返回 **TRUE** 以指示已处理请求。

有关更多详细信息，请参阅 [**视频 \_ 请求 \_ 数据包**](/windows-hardware/drivers/ddi/video/ns-video-_video_request_packet) 和 [**状态 \_ 块**](/windows-hardware/drivers/ddi/video/ns-video-_status_block) 结构。

 

