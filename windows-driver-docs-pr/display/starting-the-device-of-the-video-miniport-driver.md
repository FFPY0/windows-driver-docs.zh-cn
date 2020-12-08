---
title: 启动视频微型端口驱动程序的设备
description: 启动视频微型端口驱动程序的设备
keywords:
- 视频微型端口驱动程序 WDK Windows 2000，启动设备
- 正在启动视频微型端口驱动程序的设备
- 设备启动 WDK 视频微型端口
- 视频微型端口驱动程序 WDK Windows 2000，初始化
- 初始化视频微型端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a8ad5374d07eb00eb006c47289c37d0f46ddff5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820807"
---
# <a name="starting-the-device-of-the-video-miniport-driver"></a>启动视频微型端口驱动程序的设备


## <span id="ddk_starting_the_device_of_the_video_miniport_driver_gg"></span><span id="DDK_STARTING_THE_DEVICE_OF_THE_VIDEO_MINIPORT_DRIVER_GG"></span>


PnP 管理器发送 IRP 代码 (请参阅 [Irp 主要函数代码](../kernel/irp-major-function-codes.md)) 到请求图形适配器启动的视频端口驱动程序。 视频端口驱动程序的调度例程会调用微型端口驱动程序的 [*HwVidFindAdapter*](/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_find_adapter) 例程来响应此 IRP 代码。 以下主题讨论了某些 *HwVidFindAdapter* 任务的详细信息：

[设置视频适配器访问范围](setting-up-video-adapter-access-ranges.md)

[在注册表中设置硬件信息](setting-hardware-information-in-the-registry.md)

[更改适配器上的状态](changing-state-on-the-adapter.md)

 

