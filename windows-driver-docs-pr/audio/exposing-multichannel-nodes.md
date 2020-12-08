---
title: 公开多声道节点
description: 公开多声道节点
keywords:
- 音频属性 WDK，多通道节点
- WDM 音频属性 WDK，多通道节点
- 公开多通道节点
- 多通道节点 WDK 音频
- 节点 WDK 音频，多通道
- 最小音量级别 WDK 音频
- 最大音量级别 WDK 音频
- 基本-支持查询 WDK 音频
- 范围值 WDK 音频
- SndVol32 WDK 音频
- 多频道支持 WDK 音频
- 扬声器 WDK 音频，多通道节点
- 通道多通道支持 WDK 音频
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2a24c037c27599b84466a0e4fba7b48f56e0a923
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96784819"
---
# <a name="exposing-multichannel-nodes"></a>公开多声道节点


## <span id="exposing_multichannel_nodes"></span><span id="EXPOSING_MULTICHANNEL_NODES"></span>


在 Windows XP 之前的 Microsoft Windows 版本中，WDM 音频驱动程序没有一种简单的方法来公开以下类型的多通道节点：

[**KSNODETYPE \_ 卷**](./ksnodetype-volume.md)

[**KSNODETYPE \_ 静音**](./ksnodetype-mute.md)

[**KSNODETYPE \_ 音**](./ksnodetype-tone.md)

特别是，没有任何机制可用于在节点上显式查询它支持的通道数。 尽管存在此问题的解决方法，但存在一些缺点。 例如，客户端可以使用 [**KSPROPERTY \_ AUDIO \_ VOLUMELEVEL**](./ksproperty-audio-volumelevel.md) 属性以迭代方式查询每个通道的卷级别的卷节点 ([**KSNODETYPE \_ 卷**](./ksnodetype-volume.md)) -0、1等等--直到请求返回错误，指示不存在更多通道。 但是，这种方法需要多个查询，并且太低效，无法处理更新的多通道音频设备。 在 Windows XP 和更高版本的操作系统中，通过在 [**KSPROPERTY \_ MEMBERSHEADER**](/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_membersheader)结构的 **Flags** 成员中定义两个附加的标志位来解决此限制，属性处理程序会输出该标志来响应基本支持查询：

-   KSPROPERTY \_ 成员 \_ 标志 \_ BASICSUPPORT 多 \_ 通道

    在节点上的基本支持属性请求期间，处理程序将此标志位设置为指示 KSPROPERTY MEMBERSHEADER 的 **MembersCount** 成员 \_ 包含该节点支持的通道数。 对于 Windows Vista 和更高版本的 Windows 操作系统，必须为每个通道属性设置此标志。

-   KSPROPERTY \_ 成员 \_ 标志 \_ BASICSUPPORT \_ 统一

    处理程序在此标志位和 KSPROPERTY \_ 成员 \_ 标志 BASICSUPPORT 多通道标志位之间执行位或运算， \_ \_ 以指示单个属性值在节点中的所有通道上统一应用。 例如，如果硬件只为所有通道提供单个卷级控制，则卷节点的基本支持处理程序将设置 KSPROPERTY \_ MEMBER \_ 标志 \_ BASICSUPPORT \_ 统一标志以指示此限制。 如果未设置此标志，则每个通道的卷级别可以独立于其他通道的卷级别进行控制。

    **注意**  \_ \_ \_ \_ Windows VISTA 操作系统不使用 KSPROPERTY 成员标志 BASICSUPPORT 统一标志。

     

在适用于 Windows XP 和更高版本的微型端口驱动程序中，多通道卷节点的属性处理程序应将 KSPROPERTY \_ 成员标志设置为 \_ \_ \_ 响应 KSPROPERTY \_ 音频 \_ VOLUMELEVEL 基本支持查询。 处理程序返回一个 [**KSPROPERTY \_ 单步执行 \_ 长**](/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_stepping_long) 结构的数组-每个节点公开一个通道，并将 **MEMBERSSIZE** 设置为 **sizeof** (KSPROPERTY \_ 步进 \_ 长) 。 每个数组元素都描述了一个通道的最小和最大音量级别以及该范围内连续值之间的差异。 可以为每个单独的通道指定不同的范围，以便能够正确地公开具有非统一范围的通道。 例如，低音炮频道的范围可能不同于其他通道的范围。

下面的代码示例演示如何处理具有非统一属性值的 [音频属性的基本支持查询](basic-support-queries-for-audio-properties.md) 。 下面第一行代码中的变量 pDescription 指向数据缓冲区开头的 [**KSPROPERTY \_ 说明**](/windows-hardware/drivers/ddi/ks/ns-ks-ksproperty_description) 结构，处理程序将基本支持信息写入其中：

```cpp
  //
  // Fill in the members header.
  //
  PKSPROPERTY_MEMBERSHEADER pMembers = PKSPROPERTY_MEMBERSHEADER(pDescription + 1);

  pMembers->MembersFlags = KSPROPERTY_MEMBER_STEPPEDRANGES;
  pMembers->MembersSize = sizeof(KSPROPERTY_STEPPING_LONG);
  pMembers->MembersCount = ulNumChannels;
  pMembers->Flags = KSPROPERTY_MEMBER_FLAG_BASICSUPPORT_MULTICHANNEL;

  //
  // Fill in the stepped range with the driver default.
  //
  PKSPROPERTY_STEPPING_LONG pRange = PKSPROPERTY_STEPPING_LONG(pMembers + 1);
  pRange->Reserved = 0;

  for (ULONG i=0; i<ulNumChannels; i++)
  {
      pRange[i].Bounds.SignedMinimum = ulChannelMin[i];
      pRange[i].Bounds.SignedMaximum = ulChannelMax[i];
      pRange[i].SteppingDelta = ChannelStepping[i];
  }

  pPropertyRequest->ValueSize = sizeof(KSPROPERTY_DESCRIPTION) +
                                sizeof(KSPROPERTY_MEMBERSHEADER) + 
                                ulNumChannels * sizeof(KSPROPERTY_STEPPING_LONG);
```

下图显示了此示例的数据缓冲区的布局。 将 pDescription、pMembers 和 pRange 指针指向缓冲区内其各自的偏移量。

![说明基本支持查询的数据缓冲区布局的关系图](images/propdesc.png)

在此示例中，处理程序将 **MembersCount** 设置为 **ulNumChannels**，即通道数。 范围数组的大小（以字节为单位）为

**MembersSize** \***MembersCount**

请注意，如果 \_ \_ \_ \_ 在此示例中设置了 KSPROPERTY 成员标志 BASICSUPPORT 统一标志，则处理程序会将 \_ 数组中所有 KSPROPERTY 单步执行的 \_ 长结构设置为相同的范围。

色调节点的 [**KSPROPERTY \_ 音频 \_ 低音**](./ksproperty-audio-bass.md)、 [**KSPROPERTY \_ 音频 \_ 高音**](./ksproperty-audio-treble.md)或 [**KSPROPERTY \_ 音频 \_ MID**](./ksproperty-audio-mid.md) 属性的基本支持处理程序的运行方式类似。

如果多通道节点具有类型为 BOOL 的每个通道属性值的属性，则基本支持处理程序必须为单步范围数组填写值。 在这种情况下，处理程序会将成员设置为下面的代码示例中所示的值。 此类型属性的两个示例是静音节点的 [**KSPROPERTY \_ 音频 \_ 静音**](./ksproperty-audio-mute.md) 属性和声调节点的 [**KSPROPERTY \_ 音频 \_ 低音 \_ 提升**](./ksproperty-audio-bass-boost.md) 属性。

下面的代码示例演示如何处理多通道节点的基本支持请求，在此情况下，如果属性具有类型为 BOOL 的每个通道的属性值，则为：

```cpp
  //
  // Fill in the members header.
  //
  PKSPROPERTY_MEMBERSHEADER pMembers = PKSPROPERTY_MEMBERSHEADER(pDescription + 1);

  pMembers->MembersFlags = KSPROPERTY_MEMBER_STEPPEDRANGES;
  pMembers->MembersSize = sizeof (KSPROPERTY_STEPPING_LONG);
  pMembers->MembersCount = ulNumChannels;
  pMembers->Flags = KSPROPERTY_MEMBER_FLAG_BASICSUPPORT_MULTICHANNEL;

  pPropertyRequest->ValueSize = sizeof(KSPROPERTY_DESCRIPTION) +
                                sizeof(KSPROPERTY_MEMBERSHEADER) + 
                                ulNumChannels * sizeof(KSPROPERTY_STEPPING_LONG);

  //
  // Fill in the stepped range with values in FOR loop.
  //
  PKSPROPERTY_STEPPING_LONG pRange = PKSPROPERTY_STEPPING_LONG(pMembers + 1);
  pRange->Reserved = 0;

  for (ULONG i=0; i<ulNumChannels; i++)
  {
      pRange[i].Bounds.SignedMinimum = 0;
      pRange[i].Bounds.SignedMaximum = 1;
      pRange[i].SteppingDelta = 1;
  }
```

请注意，在上面的代码示例中，FOR 循环使用零 (0) 和一个 (1) 来设置每个通道范围的最小值和最大值。 这是因为我们要使用 BOOL 类型的每个通道属性值配置多通道节点。

如果通道属性是统一的，则可以在 KSPROPERTY \_ 成员 \_ 标志 \_ BASICSUPPORT \_ 统一标志与 KSPROPERTY \_ 成员 \_ 标志 \_ BASICSUPPORT 多 \_ 通道标志以及分配给 pMembers 成员的结果 &gt; 之间执行位或运算。 此值用于指示硬件在节点中的所有通道之间统一应用相同的属性值。

使用 KSPROPERTY \_ 成员 \_ 标志 \_ 统一和 KSPROPERTY \_ 成员标记多 \_ \_ 通道标志，无需将通道分组为成对，并为每对通道公开单独的立体声卷节点，就像在 Windows 驱动程序工具包 (WDK) 中的 Ac97 示例驱动程序中所做的那样。 由于 windows XP 之前的 Windows 版本不支持这些标志，因此，驱动程序的基本支持处理程序必须使用 [IPortClsVersion](/windows-hardware/drivers/ddi/portcls/nn-portcls-iportclsversion) 接口来查询 Portcls.sys 版本，以便确定是否使用这些标志。

拓扑分析程序 (内核模式 [WDMAud 系统驱动程序](user-mode-wdm-audio-components.md#wdmaud_system_driver)，Wdmaud.sys) 从其 WDM 音频驱动程序获取音频设备的拓扑。 分析器通过旧的 Windows 多媒体 **混音** 器 API 将该设备作为传统混音器设备公开。 在 Windows XP 和更高版本中，WDMAud 使用 KSPROPERTY \_ 成员 \_ 标志 \_ BASICSUPPORT \_ 多通道标志来确定要在 MIXERLINE 结构的 **cChannels** 成员中报告的通道数。 此外，如果节点的基本支持处理程序指定了 KSPROPERTY \_ 成员 \_ 标志 \_ BASICSUPPORT \_ 统一标志，则 WDMAud 将 \_ \_ 在相应的 CONTROLF 结构中设置 MIXERCONTROL MIXERCONTROL 统一标志。 通过此标志，应用程序可以确定它们是否可以通过主控件单独调整每个通道或所有通道。 有关 MIXERCONTROL、MIXERLINE 和 **混音** 器 API 的详细信息，请参阅 Microsoft Windows SDK 文档。

在 Windows XP 和更高版本中，SndVol32 卷控制程序 (参阅 " [托盘和 SndVol32](systray-and-sndvol32.md) ") 显示多通道设备的控件，如下图所示。

![sndvol32 "音量控制" 对话框的屏幕截图 ](images/volctrl.png)

如果 SndVol32 检测到具有两个以上通道的线条，则它会将普通平移控件替换为一个标记为 " **扬声器音量**" 的按钮，该按钮显示在上图中的主音量滑块上方。 单击 " **扬声器音量** " 按钮将显示一个对话框，其中显示特定行的所有通道的控件，如下图所示。

![带有高级音频属性的 "发言人" 对话框的屏幕截图](images/spkrvol.png)

由于 **混音** 器 API 按编号公开通道，因此它会从当前在 Windows 多媒体控制面板 ( # A0) 的 " **高级音频属性** " 对话框中选择的扬声器配置中推断通道名称。

例如，如果设备在线路上公开四个通道，并且用户选择了 "Quadraphonic 扬声器"，则通道名称将是 "左" (通道 0) ，"Right" (通道 1) ，"Back" (通道 2) ，"后端" (通道 3) ，如上图所示。 将扬声器配置更改为 "环绕声扬声器" 将导致通道映射 "左" (通道 0) 、"右" (通道 1) 、"前端中心" (通道 2) 和 "后中心" (通道 3) 。

在驱动程序级别，KSPROPERTY \_ 音频 \_ 通道 \_ CONFIG 属性使用 KSAUDIO \_ 音箱 \_ 四或 KSAUDIO 扬声器环绕的掩码值 \_ \_ ，分别表示 quadraphonic 或环绕发言人配置。 标头文件 Ksmedia 定义这些值，如下所示：

```cpp
  #define KSAUDIO_SPEAKER_QUAD      (SPEAKER_FRONT_LEFT | SPEAKER_FRONT_RIGHT | \
                                     SPEAKER_BACK_LEFT | SPEAKER_BACK_RIGHT)

  #define KSAUDIO_SPEAKER_SURROUND  (SPEAKER_FRONT_LEFT | SPEAKER_FRONT_RIGHT | \
                                     SPEAKER_FRONT_CENTER | SPEAKER_BACK_CENTER)
```

任一掩码包含四位，用于指定四个通道的扬声器位置。 无论是哪种情况，KSPROPERTY \_ AUDIO \_ VOLUMELEVEL 属性都将它们分别标识为通道0、1、2和3。

如果节点的基本支持处理程序将 KSPROPERTY 成员标志设置为 "BASICSUPPORT"，则 " \_ \_ \_ \_ **扬声器音量** " 对话框中显示的滑块会与对任何单个滑块的更改一起移动。

 

