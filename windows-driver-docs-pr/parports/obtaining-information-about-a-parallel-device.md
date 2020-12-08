---
title: 获取有关并行设备的信息
description: 获取有关并行设备的信息
keywords:
- 并行设备 WDK，获取信息
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 20cf5c405bf3cfda850a9b45755c7412832c4555
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812605"
---
# <a name="obtaining-information-about-a-parallel-device"></a>获取有关并行设备的信息





除了 [连接到并行设备](connecting-to-a-parallel-device.md)外，客户端还可以使用下列设备控制请求来获取有关并行设备的其他信息：

[**IOCTL \_ IEEE1284 \_ GET \_ 模式**](/windows-hardware/drivers/ddi/ntddpar/ni-ntddpar-ioctl_ieee1284_get_mode)

[**IOCTL \_ PAR \_ 获取 \_ 默认 \_ 模式**](/windows-hardware/drivers/ddi/ntddpar/ni-ntddpar-ioctl_par_get_default_modes)

[**IOCTL \_ PAR \_ 获取 \_ 设备 \_ CAP**](/windows-hardware/drivers/ddi/ntddpar/ni-ntddpar-ioctl_par_get_device_caps)

[**IOCTL \_ PAR \_ 是 \_ \_ 免费端口**](/windows-hardware/drivers/ddi/ntddpar/ni-ntddpar-ioctl_par_is_port_free)

[**IOCTL \_ PAR \_ 查询 \_ 设备 \_ ID \_ 大小**](/windows-hardware/drivers/ddi/ntddpar/ni-ntddpar-ioctl_par_query_device_id_size)

[**IOCTL \_ PAR \_ 查询 \_ 设备 \_ ID**](/windows-hardware/drivers/ddi/ntddpar/ni-ntddpar-ioctl_par_query_device_id)

[**IOCTL \_ PAR \_ 查询 \_ 信息**](/windows-hardware/drivers/ddi/ntddpar/ni-ntddpar-ioctl_par_query_information)

[**IOCTL \_ PAR \_ 查询 \_ 位置**](/windows-hardware/drivers/ddi/ntddpar/ni-ntddpar-ioctl_par_query_location)

[**IOCTL \_ PAR \_ 查询 \_ 原始 \_ 设备 \_ ID**](/windows-hardware/drivers/ddi/ntddpar/ni-ntddpar-ioctl_par_query_raw_device_id)

[**IOCTL \_ 序列 \_ 获取 \_ 超时**](/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_get_timeouts)

 

