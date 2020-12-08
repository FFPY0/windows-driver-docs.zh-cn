---
title: 使用 Storport 进行硬件初始化
description: 使用 Storport 进行硬件初始化
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2ca67e3259b2bf97b52c5b666bf9ff9546ade37d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835189"
---
# <a name="hardware-initialization-with-storport"></a>使用 Storport 进行硬件初始化

Storport 驱动程序遵循 SCSI 端口驱动程序的即插即用 (PnP) 初始化模型。 在驱动程序的 [**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程期间，微型端口驱动程序使用 [**HW_INITIALIZATION_DATA (STORPORT)**](/windows-hardware/drivers/ddi/storport/ns-storport-_hw_initialization_data-r1)结构来调用 [**StorPortInitialize**](/windows-hardware/drivers/ddi/storport/nf-storport-storportinitialize)例程，该结构描述了它支持的硬件。 稍后，当 PnP 管理器调用端口驱动程序的 [**StartIo**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_startio)例程时，端口驱动程序使用 [**PORT_CONFIGURATION_INFORMATION (STORPORT)**](/windows-hardware/drivers/ddi/storport/ns-storport-_port_configuration_information)结构调用微型端口驱动程序的 [**HwStorFindAdapter**](/windows-hardware/drivers/ddi/storport/nc-storport-hw_find_adapter)例程，然后调用微型端口驱动程序的 [**HwStorInitialize**](/windows-hardware/drivers/ddi/storport/nc-storport-hw_initialize)例程来初始化适配器。

大多数情况下，HW_INITIALIZATION_DATA 结构的 Storport 版本与用于 SCSI 端口的相同名称的结构相同。

正如在 [storport I/o 模型中使用映射缓冲区](use-of-mapping-buffers-in-the-storport-i-o-model.md)中所述，HW_INITIALIZATION 和 PORT_CONFIGURATION_INFORMATION 的 **MapBuffers** 成员在 Storport 情况下具有不同的含义，在这种情况下，SCSI 端口事例中的相同。
