---
title: PF 微型端口驱动程序的 INF DDInstall.HW 节
description: PF 微型端口驱动程序的 INF DDInstall.HW 节
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 267118705101f7c63a810f7cceb9459252effd59
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839887"
---
# <a name="inf-ddinstallhw-section-for-pf-miniport-drivers"></a>PF 微型端口驱动程序的 INF DDInstall.HW 节


INF <em>DDInstall</em>**。硬件** 部分通常用于在注册表中设置任何设备特定的信息，无论是使用显式 **AddReg** 指令还是 **包含** 和 **需要** 条目。

PCI Express (PCIe 的微型端口驱动程序的 INF 文件) 物理功能 (PF) 网络适配器必须具有 <em>DDInstall</em>**。** 包含以下 INF 条目的 HW 部分：

-   一个 **包含** 项，它指定 Windows 操作系统附带的 pci .inf 文件。

-   指定要包含在 pci .inf 文件中的 **PciSriovSupported** 部分的 "**需要**" 项。 本部分定义适用于网络适配器的所有 PF 微型端口驱动程序的标准 INF 设置，这些网络适配器支持 (SR-IOV) 接口的单个根 i/o 虚拟化。

下面是 <em>DDInstall</em>的一个示例 **。** PF 微型端口驱动程序的硬件部分：

``` syntax
[Device_Inst.NT.HW]

Include=pci.inf
Needs=PciSriovSupported.HW
```

有关 *DDInstall* 部分的详细信息，请参阅 [网络 INF 文件中的 DDInstall 部分](ddinstall-section-in-a-network-inf-file.md)。

有关 *DDInstall* 的详细信息。HW 部分，请参阅 [**INF DDInstall 部分**](../install/inf-ddinstall-hw-section.md)。

 

