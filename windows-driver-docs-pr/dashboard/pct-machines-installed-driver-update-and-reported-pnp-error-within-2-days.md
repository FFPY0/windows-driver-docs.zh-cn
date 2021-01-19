---
title: 安装了驱动程序更新并在安装后两天内报告 PnP 错误代码的计算机的百分比
description: 度量将 30 天滑动窗口中的遥测数据聚合为成功安装驱动程序并在安装两天内遇到 PNP 错误的计算机所占的百分比
ms.topic: article
ms.date: 05/22/2020
ms.localizationpriority: medium
ms.openlocfilehash: e1ceacc6b22713ddfafc8c029e7fbe2d730f44f0
ms.sourcegitcommit: 3af9ea49935f54b272da0b0d182e81416716f698
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2021
ms.locfileid: "98052564"
---
# <a name="percent-of-machines-that-installed-a-driver-update-and-reported-a-pnp-error-code-within-two-days-of-install"></a>安装了驱动程序更新并在安装后两天内报告 PnP 错误代码的计算机的百分比

## <a name="description"></a>说明

成功安装后，计算机可能会遇到安装后 PnP 错误，该错误会导致消极的用户体验 - 从设备未按预期方式工作到意外重启。 PNP 错误代码列表位于[设备管理器问题代码](../install/device-manager-error-messages.md)和 [Windows 支持](https://support.microsoft.com/help/310123/error-codes-in-device-manager-in-windows)。

## <a name="measure-attributes"></a>度量属性

|属性|值|
|----|----|
|受众|展开|
|时间段|30 天滑动窗口|
|度量标准|计算机的聚合|
|最小总体数量|100 台计算机|
|通过标准|<= 5% 的计算机遇到安装后 PNP 错误|
|已启用队列|是|
|每队列最小总体数量|500 台计算机|
|度量 ID|26387262|

## <a name="calculation"></a>计算

1. 度量将 30 天滑动窗口中的遥测数据聚合为成功安装驱动程序并在安装 2 天内遇到 PNP 错误的计算机所占的百分比

   a. 不计算与 30 天窗口外的安装相关联的任何 PNP 错误

2. 安装后 PNP 错误数 = 计数（在驱动程序安装两天内出现 PNP 错误的计算机数）
3. 安装后错误总数 = 计数（已成功安装驱动程序的所有计算机数）

### <a name="final-calculation"></a>最终计算

安装后 PNP 错误率 = 安装后 PNP 错误数/安装后错误总数
