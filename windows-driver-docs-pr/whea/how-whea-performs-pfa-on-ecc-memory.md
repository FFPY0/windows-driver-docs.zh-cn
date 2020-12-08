---
title: WHEA 如何在 ECC 内存上执行 PFA
description: WHEA 如何在 ECC 内存上执行 PFA
keywords:
- 预测性故障分析 (PFA) WDK WHEA，纠错代码内存
- PFA WDK WHEA，纠错代码内存
- 错误更正代码内存 WDK WHEA
- 错误更正代码内存 WDK WHEA、预测性故障分析
- 低级别硬件错误处理程序 WDK WHEA
- LLHEH WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e710c1e1d19f09c03b031b0113a394a0bc93862
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837021"
---
# <a name="how-whea-performs-pfa-on-ecc-memory"></a>WHEA 如何在 ECC 内存上执行 PFA


从 Windows 7 开始，Windows 硬件错误体系结构 (WHEA) 支持预测性故障分析 (PFA) 用于错误纠正代码 (ECC) 内存。

仅当满足以下条件时，WHEA 才会在 ECC 内存页面上执行 PFA：

-   注册表值 **MemPfaDisable** 未设置为1。

-   [ (PSHED) 插件的特定于平台的硬件错误驱动程序](platform-specific-hardware-error-driver-plug-ins2.md)之前未将 [WHEA \_ 错误 \_ 数据包](/previous-versions/windows/hardware/drivers/ff560465(v=vs.85))结构的 [**WHEA \_ 错误 \_ 数据包 \_ 标志**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_error_packet_flags)成员中的 **PlatformPfaControl** 位设置为1。 此插件在执行 PFA 时将设置此位。 有关此插件如何执行 PFA 的详细信息，请参阅 [PFA 通过 PSHED 插件执行](pfa-performed-by-a-pshed-plug-in.md)的操作。

当内存页上发生 ECC 内存错误时，WHEA 通过执行以下步骤在 ECC 内存页上执行 PFA：

1.  如果 WHEA 当前未监视 ECC 内存页，则 WHEA 会将该页添加到其监视数据库，并清除新项的错误计数和滴答计数。

    **注意**  当 ECC 内存页的滴答计数超过 **MemPfaTimeout** 注册表值时，WHEA 将停止对该页的监视。 发生这种情况时，WHEA 将从其监视数据库中删除该项。



2.  WHEA 递增 ECC 内存页的错误计数。

3.  如果错误计数超过 **MemPfaThreshold** 注册表值，WHEA 将首先调用系统内存管理器使 ECC 内存页脱机。

    **注意**  调用系统内存管理器后，不能保证 ECC 内存页将实际脱机。




然后，WHEA 将内存页添加到系统存储中 (BCD) 引导配置数据。 这会阻止在下一次系统重新启动后使用内存页。

**注意**  如果注册表值 **DisableOffline** 设置为非零值，则 WHEA 将不采用 ECC 内存页等硬件组件。 此外，如果注册表值 **MemPersistOffline** 设置为0，则 WHEA 不会将 ECC 内存页添加到 BCD 存储区。




有关 WHEA 的 PFA 注册表值的详细信息，请参阅 [WHEA 策略设置](whea-pfa-registry-settings.md)。

有关系统内存管理器的详细信息，请参阅 Windows SDK 文档中的 [内存管理](/windows/win32/memory/memory-management) 。
