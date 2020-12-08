---
title: PCM 高位深度流数据格式
description: PCM 高位深度流数据格式
keywords:
- PCM 高 bitdepth 流数据格式 WDK
- 高 bitdepth 流数据格式 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8db538fdd1ebedf58c9c12427f2b55b43c9d7423
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800967"
---
# <a name="pcm-high-bitdepth-stream-data-format"></a>PCM 高位深度流数据格式


## <span id="pcm_high_bitdepth_stream_data_format"></span><span id="PCM_HIGH_BITDEPTH_STREAM_DATA_FORMAT"></span>


此示例使用 [**KSDATAFORMAT \_ WAVEFORMATEX**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-ksdataformat_waveformatex) 结构的扩展版本来描述 PCM bitdepth 流的数据格式。 这类似于 PCM 多通道示例，但的值除外，如下所示 `Format.wBitsPerSample` `Format.wValidBitsPerSample` 。

```cpp
  DataFormat.FormatSize  = sizeof(KSDATAFORMAT) + sizeof(WAVEFORMATEXTENSIBLE);
 DataFormat.Flags       = 0;
  DataFormat.SampleSize  = 0;
  DataFormat.Reserved    = 0;
  DataFormat.MajorFormat = STATICGUIDOF(KSDATAFORMAT_TYPE_AUDIO);
  DataFormat.SubFormat   = STATICGUIDOF(KSDATAFORMAT_SUBTYPE_PCM);
 DataFormat.Specifier   = STATICGUIDOF(KSDATAFORMAT_SPECIFIER_WAVEFORMATEX);
  Format.wFormatTag      = WAVE_FORMAT_EXTENSIBLE;
  Format.nChannels       = 4;
  Format.nSamplesPerSec  = 44100;
  Format.nAvgBytesPerSec = 529200;
  Format.nBlockAlign     = 8;
  Format.wBitsPerSample  = 24;
  Format.cbSize          = sizeof(WAVEFORMATEXTENSIBLE) - sizeof(WAVEFORMATEX);
  Format.wValidBitsPerSample = 20;
  Format.dwChannelMask   = KSAUDIO_SPEAKER_SURROUND;
  Format.SubFormat       = KSDATAFORMAT_SUBTYPE_PCM;
```

 

