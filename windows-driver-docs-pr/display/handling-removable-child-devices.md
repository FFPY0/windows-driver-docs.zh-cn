---
title: 处理可移动子设备
description: 处理可移动子设备
keywords:
- 可移动子设备 WDK Windows 2000 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1b59c4d164671ae453be90c3bf45715b5a195e72
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839107"
---
# <a name="handling-removable-child-devices"></a>处理可移动子设备


视频微型端口驱动程序应检测到使用另一个类似设备更改了可移动子设备，以便驱动程序可以阻止即插即用 (PnP) 使用原始子设备的数据。 例如，当用户切换到监视器时，视频微型端口驱动程序应检测到该驱动程序。

如果附加监视器的扩展显示信息数据 (EDID) 在对视频微型端口驱动程序的 [*HwVidGetVideoChildDescriptor*](/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_get_child_descriptor) 功能的连续调用之间发生更改，而不是将原始监视器堆栈撕裂并为新监视器生成新堆栈，则视频端口驱动程序会修改当前堆栈的状态。 尽管图形子系统可以确定新的监视器的功能，因为原始堆栈未关闭，但其他操作系统组件 (如，PnP) 使用原始监视器的功能数据。

视频微型端口驱动程序可以检测对连接的监视器的更改，并执行以下操作之一来阻止 PnP 使用原始监视器的数据：

1.  视频微型端口驱动程序可以报告不存在监视器，从而强制断开以前的监视器堆栈。 然后，若要强制视频端口驱动程序重新枚举子设备，以便报告新监视器，视频微型端口驱动程序将调用 [**VideoPortEnumerateChildren**](/windows-hardware/drivers/ddi/video/nf-video-videoportenumeratechildren) 函数。 视频微型端口驱动程序应调用 **VideoPortEnumerateChildren** ，以便仅在报告监视器断开连接完成的第一个枚举后计划子设备的重新枚举。

2.  在适当的计算机和监视器配置 (查看以下异常) ，视频微型端口驱动程序可以通过将新监视器的信息返回到 *HwVidGetVideoChildDescriptor* 指向的 *pChildDescriptor* 参数的缓冲区中来响应其 [*HwVidGetVideoChildDescriptor*](/windows-hardware/drivers/ddi/video/nc-video-pvideo_hw_get_child_descriptor)函数。 但是，视频微型端口驱动程序必须在 *UId* 参数指向的变量中为新监视器指定32位 *设备 ID* 。 此值必须与用于以前的监视器的视频微型端口驱动程序的值不同。

对于高级配置和电源接口 (ACPI) 枚举监视器，第一种机制通常更可取，因为32位设备 Id 与 BIOS 实现相关联。 因此，可能无法指定其他32位设备 ID。

