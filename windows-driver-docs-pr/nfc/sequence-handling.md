---
title: NFC CX 序列处理
description: 有关通过注册 NFC CX 公开的特定驱动程序序列来支持非标准 NCI 扩展的信息。
keywords:
- NFC
- 近场通信
- 近程
- 近场邻近感应
- NFP
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21ed8e10608b4058c0a986a5f12479543285578b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812709"
---
# <a name="nfc-cx-sequence-handling"></a>NFC CX 序列处理

由不同供应商提供的 NFCC 固件实现的大多数非标准 NCI 功能和扩展与芯片组配置、固件下载和硬件优化相关。 NFC 客户端驱动程序可以通过注册 NFC CX 公开的特定驱动程序序列来支持这些非标准扩展。 客户端驱动程序通过 [**NfcCxRegisterSequenceHandler**](/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxregistersequencehandler) 函数注册特定顺序处理程序。 它通常在初始化期间完成，并应在 [**NfcCxDeviceInitialize**](/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxdeviceinitialize)后调用。 在设备关闭期间，通过调用 [**NfcCxUnRegisterSequenceHandler**](/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxunregistersequencehandler) 注销这些处理程序。 在调用客户端驱动程序的序列处理程序回调后，NFC CX 驱动程序将不会发出任何 NCI 命令，直到 NFC 客户端驱动程序完成其处理。 这些序列处理程序回调设计为是异步的，因此，客户端可以在将 NFC CX 通知完成后，向控制器发出任意数量的 i/o 请求。 NFC CX 使用监视程序计时器机制来确定挂起状态。 如果监视程序计时器在客户端完成序列处理程序之前过期，则会触发 bug 检查，且 umdf 框架终止了 UMDF 主机进程。

下面是在将任何其他逻辑作为序列处理程序的一部分实现时 NFC 客户端驱动程序的要求：

- 处理这些序列时，NFC 客户端发送的任何 NCI 命令都应确保不违反 NFC CX 指定的当前状态的完整性。 因此，NFC 客户端必须处理此要求，以确保 NFC 设备正常运行。 例如，在处理初始化完成序列时，客户端驱动程序不应发出 NCI CORE \_ reset \_ CMD 来重置芯片集。
- NFC 客户端驱动程序需要确保其向下发送到控制器的 NCI 命令生成的 NCI 响应和通知不会发送到 NFC CX 的 [**NfcCxNciReadNotification**](/windows-hardware/drivers/ddi/nfccx/nf-nfccx-nfccxncireadnotification) 函数。 这是必需的，因为在此情况下，NFC CX NCI 状态机将不会与它与 NFCC 交换的命令同步。

## <a name="related-topics"></a>相关主题

[NFC 设备驱动程序接口 (DDI) 概述](/windows-hardware/drivers/ddi/_nfpdrivers)  
[ (CX) 参考的 NFC 类扩展](/windows-hardware/drivers/ddi/nfccx)
