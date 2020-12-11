---
title: 硬件通知设计指南
description: 以标准化方式介绍对主要按钮（电源、Windows、音量和旋转锁）和其他指示器的支持，另外还介绍了已关联的相应 Windows 工程指南 (WEG)。
ms.assetid: E18DAA6C-C64D-40B3-A112-682A935655D0
ms.date: 06/16/2017
ms.topic: article
ms.prod: windows-hardware
ms.technology: windows-devices
ms.openlocfilehash: 54c4317a30f501fab7e7637c87904bbc8bd09816
ms.sourcegitcommit: e47bd7eef2c2b89e3417d7f2dceb7c03d894f3c3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/10/2020
ms.locfileid: "97090755"
---
# <a name="hardware-notifications-design-guide"></a>硬件通知设计指南

以标准化方式介绍对主要按钮（电源、Windows、音量和旋转锁）和其他指示器的支持，另外还介绍了已关联的相应 Windows 工程指南 (WEG)。

## <a name="in-this-section"></a>在本节中

|主题|说明|
|----|----|
|[GPIO 按钮和指示器实现指南](gpio-buttons-and-indicators-implementation-guide-for-windows-8-1.md)|Windows 8 通过 HID 微型端口类驱动程序引入了对常规 I/O (GPIO) 按钮和指示器的支持。 目标是以标准化方式提供对主要按钮（电源、Windows、音量和旋转锁）的支持，另外还介绍了已关联的相应 Windows 工程指南 (WEG)。 Windows 8.1 专注于增强端到端用户体验的质量以及统一各种创新性外形规格的行为。|
|[GPIO 按钮和指示器实现测试](gpio-buttons-and-indicators-supplemental-certification-testing-for-windows-8-1.md)|本主题介绍适用于硬件按钮和指示器的 Windows 8.1 测试方案，目的是确保在使用不同外形规格时获得理想的用户体验。|
|[硬件通知支持](hardware-notifications-support.md)|Windows 10 版本 1709 的基础结构可以为 LED 和振动机制等通知组件提供不区分硬件的支持。 实现此支持的方式是引入内核模式驱动程序框架 (KMDF) 类扩展，该扩展专用于硬件通知组件，因此可以快速开发客户端驱动程序。 KMDF 类扩展实质上是 KMDF 驱动程序，它为给定的设备类提供一组定义的功能，类似于 Windows 驱动程序模型 (WDM) 中的端口驱动程序。 此部分概述硬件通知类扩展的体系结构。 有关 KMDF 的其他信息，请参阅 [Using WDF to Develop a Driver](../wdf/using-the-framework-to-develop-a-driver.md)（使用 WDF 来开发驱动程序）。|

