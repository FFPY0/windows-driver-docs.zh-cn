---
title: 内容 ID 和内容权限
description: 内容 ID 和内容权限
keywords:
- 内容权限 WDK 音频
- 内容 Id WDK 音频
- 数字 Rights Management WDK 音频，内容 Id
- DRM WDK 音频，内容 Id
- 数字 Rights Management WDK 音频，内容权限
- DRM WDK 音频，内容权限
- 标识符 WDK 音频
- 混合流 WDK 音频
- DigitalOutputDisable 标志
- CopyProtect 标志
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e901faae1a4136b27ed1252d4315887ffab3f3d4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784909"
---
# <a name="content-ids-and-content-rights"></a>内容 ID 和内容权限


## <span id="content_ids_and_content_rights"></span><span id="CONTENT_IDS_AND_CONTENT_RIGHTS"></span>


内容 ID (标识符) 是一个 ULONG 值， [DRMK 系统驱动程序](kernel-mode-wdm-audio-components.md#drmk_system_driver) 将在运行时生成该值，以便在音频数据流中标识馈送到特定 pin 的受 DRM 保护的内容。

内容权限是内容提供商向用户授予的用于播放和复制受 DRM 保护内容的权限的数字表示形式。 内容权限以 DRMK 传递到音频驱动程序的 [**DRMRIGHTS**](/windows-hardware/drivers/ddi/drmk/ns-drmk-tagdrmrights) 结构的形式指定。

DRMRIGHTS 包含两个标志： **DigitalOutputDisable** 和 **CopyProtect**。 如果设置了 **DigitalOutputDisable** 标志，则驱动程序必须通过 S/PDIF 连接器禁用连接到外部设备 (的任何数字输出，例如) 。 如果设置了 **CopyProtect** 标志，则驱动程序必须禁用一些功能，这些功能可能会允许安全内容的持久性副本保存到磁盘或任何其他形式的非易失性存储。 例如，典型的音频硬件允许通过捕获通道路由播放信号。 如果此信号采用数字格式，则捕获的信号可能是输入信号的完美数字副本。 如果播放组合包含的数据来自设置了 **CopyProtect** 标志的任何流，则驱动程序必须将播放捕获路径设为静音。

与 DRM 兼容的音频驱动程序必须支持其 WaveCyclic 和 WavePci 微型端口驱动程序对象上的 [IDrmAudioStream](/windows-hardware/drivers/ddi/drmk/nn-drmk-idrmaudiostream) 接口，这些对象公开用于呈现音频数据的接收器 pin。 为了从驱动程序获取对 **IDrmAudioStream** 对象的引用，DRMK 对该 Pin 调用 **QueryInterface** 方法。 Pin 具有 [IMiniportWaveCyclicStream](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavecyclicstream) 或 [IMiniportWavePciStream](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavepcistream)类型的接口。 除了) 三个 **IUnknown** 方法之外， **IDrmAudioStream** 接口仅支持一个方法 [**： IDrmAudioStream：： SetContentId**](/windows-hardware/drivers/ddi/drmk/nf-drmk-idrmaudiostream-setcontentid) (。 当 DRMK 调用 **SetContentId** 时，它会传入内容 ID 和内容权限，驱动程序会将该内容与 pin 的数据流相关联。

WaveCyclic 或 WavePci 微型端口驱动程序可以通过 [IDrmPort2](/windows-hardware/drivers/ddi/portcls/nn-portcls-idrmport2) 接口访问 drm 函数，而不是直接在 Drmk.sys 中调用 drm 函数 (**IDrmPort2** 是从基类 [IDrmPort](/windows-hardware/drivers/ddi/portcls/nn-portcls-idrmport)) 派生的。 在 Microsoft Windows XP 和更高版本中，WaveCyclic 和 WavePci 端口驱动程序支持 **IDrmPort2**。 微型端口驱动程序通过使用 REFIID IID IDrmPort2 调用端口对象的 **QueryInterface** 方法，获取对端口驱动程序的 **IDrmPort2** 接口的引用 \_ 。

某些音频驱动程序支持硬件混合，可以同时处理多个输入数据流。 这种类型的驱动程序必须跟踪单个流的内容 Id 和所有流的复合内容权限。 驱动程序调用 [**IDrmPort：： CreateContentMixed**](/windows-hardware/drivers/ddi/portcls/nf-portcls-idrmport-createcontentmixed) 来确定混合流的复合权限，并创建内容 ID 来标识该流。 当驱动程序使用内容 ID 完成后，必须调用 [**IDrmPort：:D estroycontent**](/windows-hardware/drivers/ddi/portcls/nf-portcls-idrmport-destroycontent) 删除内容 id。

每次向混音器中添加或删除输入流时，驱动程序必须删除旧组合的内容 ID，并为新的组合创建新的内容 ID。 在删除旧内容 ID 之前，驱动程序必须首先将新的内容 ID 成功转发到其之前转发旧内容 ID 的所有流。 有关详细信息，请参阅 [转发 DRM 内容 id](forwarding-drm-content-ids.md)。

 

