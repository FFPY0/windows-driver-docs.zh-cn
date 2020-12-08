---
title: COPP 简介
description: COPP 简介
keywords:
- 复制保护 WDK COPP，关于 COPP
- 视频复制保护 WDK COPP，关于 COPP
- COPP WDK DirectX VA，关于 COPP
- 受保护的视频 WDK COPP，关于 COPP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bb1fde668d162a058c042678bbf0c78fc7f4b339
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792301"
---
# <a name="introduction-to-copp"></a>COPP 简介


## <span id="ddk_introduction_to_the_certified_output_protection_protocol_gg"></span><span id="DDK_INTRODUCTION_TO_THE_CERTIFIED_OUTPUT_PROTECTION_PROTOCOL_GG"></span>


**本部分仅适用于 Windows Server 2003 SP1 及更高版本以及 Windows XP SP2 及更高版本。**

COPP 提供了一种机制，用于将复制保护应用到由图形适配器输出的视频。 COPP 提供一种通用协议，用于以一种更受保护的方式将各种链接保护要求发送到图形适配器，而不是使用 [**ioctl \_ 视频 \_ 句柄 \_ VIDEOPARAMETERS**](/windows-hardware/drivers/ddi/ntddvdeo/ni-ntddvdeo-ioctl_video_handle_videoparameters) i/o 控制 (ioctl) 代码。

以下主题介绍 COPP：

[COPP 使用的加密基元](cryptographic-primitives-used-by-copp.md)

[通过安全通道进行通信](communicating-through-a-secure-channel.md)

[支持 COPP 所要满足的图形适配器输出要求](graphics-adapter-output-requirements-to-support-copp.md)

 

