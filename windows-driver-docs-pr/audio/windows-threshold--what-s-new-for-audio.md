---
title: Windows 10 音频驱动程序的新增功能
description: 本主题提供有关 Windows 10 的音频新增功能的高级摘要。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b6d0e71d9f675e49e8bb4430c5a6a145f0ca3a59
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798715"
---
# <a name="windows-10-whats-new-for-audio-drivers"></a>Windows 10：音频驱动程序的新增功能

本主题提供有关 Windows 10 的音频新增功能的高级摘要。

## <a name="feature-summary"></a>功能摘要

下面是 Windows 10 中新增的音频功能。

- [实现音频模块通信](implementing-audio-module-communication.md)

- [低延迟音频改进](#low-latency-audio-improvements)

- [信号处理模式和音频类别](#signal-processing-modes-and-audio-categories)

- [硬件卸载 APO 效果](#hardware-offloaded-apo-effects)

- [Cortana 语音激活](#cortana-voice-activation---wake-on-voice)

- [适用于音频的 Windows 通用驱动程序](#windows-universal-drivers-for-audio)

- [音频驱动程序的资源管理](#resource-management-for-audio-drivers)

- [用于音频驱动程序的 PNP 重新平衡](#pnp-rebalance-for-audio-drivers)

## <a name="low-latency-audio-improvements"></a>低延迟音频改进

音频延迟是指在该时间内创建声音和听到声音的延迟时间。 对于几个关键方案（如下所示），具有较低的音频延迟非常重要。

- Pro 音频
- 音乐创建和混合
- Skype 等通信
- 虚拟和增强的现实
- 游戏

设备的总延迟是以下组件的延迟的总和：

- 操作系统
- 音频处理对象
- 音频驱动程序
- 音频硬件

在 Windows 10 中，执行此操作是为了降低 OS 中的延迟。 如果没有任何驱动程序更改，Windows 10 中的应用程序将遇到 4.5 m32-16ms 的低延迟。 此外，如果驱动程序已更新为利用使用小型缓冲区处理音频数据的新低延迟 DDIs，则延迟将更多。 如果驱动程序支持3ms 音频缓冲区，则往返延迟为 ~ 10ms。

![显示应用、音频引擎驱动程序和 h/w 的低延迟音频堆栈关系图](images/low-latency-audio-stack-diagram-1.png)

音频堆栈支持多个数据包大小和动态数据包大小调整，以便根据用户的情况在延迟和电源之间进行权衡。 此外，流将按优先顺序排列，以确保高优先级流 (例如，电话呼叫) 具有专用资源。

为了使音频驱动程序支持低延迟，Windows 10 提供了以下三个新功能：

1. \[必需 \] 声明每个模式所支持的最小缓冲区大小。
2. \[可选，但建议 \] 改善驱动程序和操作系统之间数据流的协调。
3. \[可选，但建议 \] (中断、线程) 注册驱动程序资源，以便在低延迟方案中可由 OS 保护这些资源。
有关详细信息，请参阅 [低延迟音频](low-latency-audio.md)。

## <a name="signal-processing-modes-and-audio-categories"></a>信号处理模式和音频类别

### <a name="signal-processing-modes"></a>信号处理模式

驱动程序声明每个设备支持的音频信号处理模式。

应用程序)  (选定的音频类别映射到 (驱动程序) 定义的音频模式。 Windows 定义了七种音频信号处理模式。 Oem 和 Ihv 可以确定要实现的模式。 下表汇总了这些模式。

|“模式”|呈现/捕获|描述|
|----|----|----|----|
|原始|推送、请求和匿名|Raw 模式指定不应对流应用任何信号处理。 应用程序可以请求完全不动并执行其自己的信号处理的原始流。|
|默认|推送、请求和匿名|此模式定义默认音频处理。|
|部|呈现|电影音频播放|
|许可证|推送、请求和匿名|音乐音频播放 (大多数媒体流的默认值) |
|语速|捕获|人为语音捕获 (例如，Cortana 的输入) |
|联系|推送、请求和匿名|VOIP 渲染和捕获 (例如 Skype、Lync) |
|提醒|呈现|铃声、警报、警报等。|

音频设备驱动程序需要至少支持 Raw 模式或默认模式。 支持附加模式是可选的。

用于语音、电影、音乐和通信的专用模式。 音频驱动程序将能够根据流类型定义不同类型的音频格式和处理。

### <a name="audio-categories"></a>音频类别

下表显示了 Windows 10 中的音频类别。

为了通知系统有关音频流的使用情况，应用程序可以选择使用特定的音频流类别标记流。 在 Windows 10 中，有九个音频流类别。

|Category|描述|
|----|----|
| 电影\*        | 带有对话框 (的电影、视频替换 ForegroundOnlyMedia)                                               |
| 媒体\*        | Media 播放 (的默认类别替换 BackgroundCapableMedia)                                  |
| 游戏聊天\*    | 用户之间的游戏间通信 (Windows 10 中的新类别)                                       |
| 语音\*       | 语音输入 (例如) 和输出 (例如，导航应用) 在 Windows 10 (新类别)  |
| 通信 | VOIP，实时聊天                                                                                  |
| 警报         | 警报，响铃音，通知                                                                       |
| 声音效果  | 嘟嘟声、dings 等                                                                                     |
| 游戏媒体     | 游戏音乐                                                                                         |
| 游戏效果   | 球弹跳，车载声音，项目符号，等等。                                                      |
| 其他          | 未分类的流                                                                                 |

\* Windows 10 中的新增项。

有关详细信息，请参阅 [音频信号处理模式](audio-signal-processing-modes.md) 和 [音频处理对象体系结构](audio-processing-object-architecture.md)。

## <a name="hardware-offloaded-apo-effects"></a>硬件卸载 APO 效果

Windows 10 支持硬件卸载的 APO 效果。 可以加载到卸载 pin 的顶部。 这允许在软件和硬件中进行音频处理。 此外，处理可以动态更改。 当 DSP 中的负载增加时，可以将部分或全部处理从软件 APO 移到 DSP，然后再移回到软件 APO。

有关详细信息，请参阅 [实现硬件卸载的 APO 效果](implementing-hardware-offloaded-apo-effects.md)。

## <a name="cortana-voice-activation---wake-on-voice"></a>Cortana 语音激活-语音唤醒

Cortana，个人助手技术最初 demonstarted 于2013的 Microsoft BUILD 开发人员大会。 语音激活是一项功能，使用户能够通过口述特定短语 "你好 Cortana" 从各种设备电源状态调用语音识别引擎。 "你好 Cortana" 语音激活 (VA) 功能使用户能够快速地利用体验 (例如，Cortana) 活动上下文之外 (例如，当前在屏幕上使用语音) 的内容。 当屏幕关闭、空闲或处于完全活动状态时，该功能将针对方案。 如果硬件支持缓冲，则用户可以将关键短语和命令短语一起链接在一起。 这可以提高用户的端到端唤醒体验。 有关详细信息，请参阅 [语音激活](voice-activation.md)。

## <a name="windows-universal-drivers-for-audio"></a>适用于音频的 Windows 通用驱动程序

Windows 10 支持适用于 PC 的一个驱动程序模型，2：1个适用于手机和小屏幕平板电脑的 Windows 10。 这意味着 Ihv 可以在一个平台上开发其驱动程序，并且该驱动程序在 (台式机、笔记本电脑、平板电脑、手机) 的所有设备中运行。 这样就缩短了开发时间和成本。

若要开发通用音频驱动程序，请使用以下工具：

1. Visual Studio 2015：新的驱动程序设置允许将 "目标平台" 设置为 "通用" 以创建多平台驱动程序。
2. APIValidator：这是一个 WDK 工具，用于检查驱动程序是否是通用的，并突出显示需要更新的调用。
3. GitHub 中的音频示例： sysvad 和 SwapAPO 已转换为通用驱动程序。
有关详细信息和 GitHub 示例代码的指针，请参阅 [适用于音频的通用 Windows 驱动程序](audio-universal-drivers.md)。

## <a name="resource-management-for-audio-drivers"></a>音频驱动程序的资源管理

在成本较低的移动设备上创建良好的音频体验的一个挑战是，某些设备有多种并发约束。 例如，设备可能只能同时播放最多6个音频流，且仅支持2个卸载流。 如果移动设备上存在活动电话呼叫，则设备可能仅支持2个音频流。 当设备正在捕获音频时，设备只能播放最多4个音频流。

Windows 10 包含一种机制，用于表达并发约束，以确保高优先级的音频流和移动电话呼叫能够播放。 如果系统资源不足，则终止低优先级流。 此机制仅适用于不在台式机或笔记本电脑上的手机和平板电脑。

有关详细信息，请参阅 [音频硬件资源管理](audio-hardware-resource-management.md)。

## <a name="pnp-rebalance-for-audio-drivers"></a>用于音频驱动程序的 PNP 重新平衡

对于需要重新分配内存资源的某些 PCI 方案，将使用 PNP 重新平衡。 在这种情况下，将卸载某些驱动程序，然后在不同的内存位置重新加载这些驱动程序，以便创建可用的连续内存空间。 可在两种主要方案中触发重新平衡：

1. PCI 热插拔：用户插入设备，PCI 总线没有足够的资源来加载新设备的驱动程序。 属于此类别的设备的一些示例包括闪电、USB-C 和 NVME 存储。 在这种情况下，需要重新排列和合并内存资源 (重新平衡) ，以支持添加其他设备。
2. PCI resizeable 竖线：在内存中成功加载设备的驱动程序后，它会请求其他资源。 设备的一些示例包括高端图形卡和存储设备。
有关详细信息，请参阅 [实现 PortCls 音频驱动程序的 PnP 再平衡](implement-pnp-rebalance-for-portcls-audio-drivers.md)。
