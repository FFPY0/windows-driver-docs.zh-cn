---
title: SCSI 端口的可以与 SCSI 端口微型端口驱动程序交互的接口
description: SCSI 端口的可以与 SCSI 端口微型端口驱动程序交互的接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 36a42ea0b5011ba53bfa900c6984464793fb4186
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839405"
---
# <a name="scsi-ports-interface-with-scsi-port-miniport-drivers"></a>SCSI 端口的可以与 SCSI 端口微型端口驱动程序交互的接口


## <span id="ddk_scsi_port_s_interface_with_scsi_port_miniport_drivers_kg"></span><span id="DDK_SCSI_PORT_S_INTERFACE_WITH_SCSI_PORT_MINIPORT_DRIVERS_KG"></span>


SCSI 端口驱动程序和 SCSI 端口微型端口驱动程序之间的通信是通过 SCSI 请求块 (SRBs) 和微型端口驱动程序回调例程来进行的。 有关 SCSI 端口微型端口驱动程序回调例程的详细讨论，请参阅 [Scsi 微型端口驱动程序](scsi-miniport-drivers.md)。

有关各个 SRB 函数、SRB 标志和 SRB 状态值的概述和定义，请参阅 [**SCSI \_ REQUEST \_ BLOCK**](/windows-hardware/drivers/ddi/srb/ns-srb-_scsi_request_block)。

有关微型端口驱动程序必须如何响应每个单独的 SRB 函数的讨论，请参阅 [SCSI 微型端口驱动程序的 HwScsiStartIo 例程](scsi-miniport-driver-s-hwscsistartio-routine.md)。

SCSI 端口会以同步方式将 SRBs 转发到 SCSI 端口微型端口驱动程序，但适配器支持标记的队列除外。 支持标记队列的主机总线适配器可以在内部对请求进行排队，并按 SCSI 端口分配给每个请求的标记指示的顺序进行处理。  (SRB) 结构的 [**scsi \_ 请求 \_ 块**](/windows-hardware/drivers/ddi/srb/ns-srb-_scsi_request_block) 包含两个成员，scsi 端口驱动程序使用该成员指定如何在主机适配器的内部队列中对 SRBs 排序： **QueuedTag** 和 **QueueAction**。 SCSI 端口向每个 SRB 的 **QueuedTag** 成员分配一个计数或 *"标记"* 值，指示适配器处理数据包的顺序。 标记值还允许 SCSI 端口跟踪哪些 SRBs 已成功完成，哪些 SRBs 已超时。

**QueueAction** 成员分配有以下值之一：

SRB \_ 简单 \_ 标记 \_ 请求

\_ \_ \_ 队列 \_ 标记 \_ 请求的 SRB 头

SRB \_ 排序 \_ 队列 \_ 标记 \_ 请求

有关这些值的说明，请参阅 SCSI-3 规范。

 

