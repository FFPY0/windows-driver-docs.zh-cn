---
title: AVStream 驱动程序示例
description: 此目录中的 AVStream 驱动程序示例提供了为设备编写自定义流媒体驱动程序的起点。
ms.date: 11/15/2019
ms.localizationpriority: medium
ms.openlocfilehash: 3142000bfa41afb69891dab0f332887e5687e66f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785675"
---
# <a name="avstream-driver-samples"></a>AVStream 驱动程序示例

此目录中的 AVStream 驱动程序示例提供了为设备编写自定义流媒体驱动程序的起点。

| 示例 | 说明 |
| --- | --- |
| [AvsCamera-AVStream 相机示例驱动程序](/samples/microsoft/windows-driver-samples/avscamera) | 为以 pin 为中心的 AVStream 捕获驱动程序提供适用于模拟的前端和后端摄像机，该驱动程序在 RGB24、RGB32、YUY2 和 NV12 格式的不同帧速率下执行模拟捕获。 |
| [AVStream 模拟硬件示例驱动程序 (Avshws) ](/samples/microsoft/windows-driver-samples/avstream-simulated-hardware-sample-driver-avshws) | 模拟的硬件示例驱动程序，提供了以 pin 为中心的捕获驱动程序来模拟 AV 捕获硬件。 |
| [AVStream 的以筛选器为中心的模拟捕获示例驱动程序 (Avssamp) ](/samples/microsoft/windows-driver-samples/avstream-filter-centric-simulated-capture-sample-driver-avssamp/) | 包含功能音频的 AVStream 筛选器中心模拟捕获示例驱动程序。 |
| [驱动程序设备转换示例](/samples/microsoft/windows-driver-samples/driver-device-transform-sample) | 驱动程序设备转换的演示示例，该转换使用媒体基础在处理基于 Avstream 的相机设备的进程中加载。 |
| [驱动程序 MFT 示例](/samples/microsoft/windows-driver-samples/driver-mft-sample) | 用于照相机的 UWP 设备应用的驱动程序 MFT。 驱动程序 MFT 是在捕获视频时用于特定相机的媒体基础转换。 |
