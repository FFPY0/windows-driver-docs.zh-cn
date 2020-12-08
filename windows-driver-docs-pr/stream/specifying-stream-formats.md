---
title: 指定流格式
description: 指定流格式
keywords:
- 视频捕获 WDK AVStream，流格式
- 捕获视频 WDK AVStream，流格式
- 流格式化 WDK 视频捕获
- 格式化 WDK 视频捕获
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55e50474f50e66654ef29a3e3bf5891975004449
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806611"
---
# <a name="specifying-stream-formats"></a>指定流格式


通常，DirectShow 和内核流共享媒体格式定义和流式处理约定。 在内核模式和用户模式组件所使用的命名约定方面，这种一致性会略有不同。 内核模式中使用的许多媒体格式和 GUID 定义都具有 *前缀 \_ KS* ，但与它们的用户模式对应项完全相同。 例如，内核模式结构（ [**KS \_ BITMAPINFOHEADER**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_bitmapinfoheader)）的 Win32 用户模式版本为 BITMAPINFOHEADER。

视频捕获微型驱动程序使用 [**KSDATAFORMAT**](/windows-hardware/drivers/ddi/ks/ns-ks-ksdataformat) 结构描述特定流格式。 但是，微型驱动程序还可以通过指定 [**KSDATARANGE**](/previous-versions/ff561658(v=vs.85)) 结构的数组来公开大量可能的流格式。 KSDATARANGE 结构描述了图像特征，如颜色格式、位深度以及裁剪和缩放可能。

单个 KSDATARANGE 结构可以描述上千个潜在的 KSDATAFORMAT 结构。 例如，KSDATARANGE 结构可以指定 RGB24 样本的视频流，其中最小维度为160x120 像素，最大维度为720x480 像素，x 和 y 维中的粒度步进大小值为1。 从此，应用程序可以通过唯一的 KSDATAFORMAT 结构请求200000多个可能的输出图像维度。

DirectShow 使用类似于 KSDATAFORMAT 的结构来定义流格式。 例如：

```cpp
typedef struct  _AMMediaType    {
    GUID majortype;            // Same as KSDATAFORMAT.MajorFormat
    GUID subtype;              // Same as KSDATAFORMAT.SubFormat
    BOOL bFixedSizeSamples;
    BOOL bTemporalCompression;
    ULONG lSampleSize;         // Same as KSDATAFORMAT.SampleSize
    GUID formattype;           // Same as KSDATAFORMAT.Specifier
    IUnknown __RPC_FAR *pUnk;
    ULONG cbFormat;
    BYTE *pbFormat;
 } AM_MEDIA_TYPE;
```

尽管命名约定不同，但内核模式 KSDATARANGE/KSDATAFORMAT 和用户模式 AM 媒体类型结构中使用的 Guid \_ \_ 是相同的。

**注意**： KSDATAFORMAT 结构的 **SubFormat** 成员的低序位四个字节 (与 AM MEDIA TYPE 用户模式结构的 **子类型** 成员相似 \_ \_) 应与 [**KS \_ BITMAPINFOHEADER**](/windows-hardware/drivers/ddi/ksmedia/ns-ksmedia-tagks_bitmapinfoheader)结构的 **biCompression** 成员中使用的 FOURCC 值相匹配。 这些字节以相反顺序保存描述格式的十六进制 ASCII 字符。

例如，以下 GUID 对应于 YVU9 FOURCC 视频格式：

```Text
39555659-0000-0010-8000-00AA00389B71
      59 = 'Y'
    56 = 'V'
  55 = 'U'
39 = '9'
```
