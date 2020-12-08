---
title: 使用 I2C 来与子设备通信
description: 使用 I2C 来与子设备通信
keywords:
- I2C WDK 视频微型端口
- 视频微型端口驱动程序 WDK Windows 2000，子设备
- 子设备 WDK 视频微型端口，使用 I2C 进行通信
- 视频微型端口驱动程序 WDK Windows 2000，I2C
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 23289aaa9f63cafb6b558f1d0eb677c390ea161d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803888"
---
# <a name="using-i2c-to-communicate-with-a-child-device"></a>使用 I2C 来与子设备通信


## <span id="ddk_using_i2c_to_communicate_with_a_child_device_gg"></span><span id="DDK_USING_I2C_TO_COMMUNICATE_WITH_A_CHILD_DEVICE_GG"></span>


在 Microsoft Windows XP 和更高版本中，在即插即用 manager 枚举视频适配器的子设备后，微型端口驱动程序可以使用 I i2c 协议与 *I2C* 总线上适配器的子设备通信。 可以通过微型端口驱动程序所公开的软件接口，在 I i2c 总线上的这些设备之间进行通信， (如 [与子设备的驱动程序通信](communicating-with-the-driver-of-a-child-device.md)) 中所述。 微型端口驱动程序可以通过视频端口驱动程序公开的新硬件接口，在 I i2c 总线上的设备之间发起物理通信。 如果微型端口驱动程序需要 (通常是图形芯片) ，才能在 I i2c 总线上从物理子设备进行读取或写入，则可以使用视频端口驱动程序的 [**VideoPortQueryServices**](/windows-hardware/drivers/ddi/video/nf-video-videoportqueryservices) 例程提供的硬件 I i2c 接口。 请注意，基于 I i2c 总线的这种通信严格限制为同一 i2c 总线上的硬件设备。 强烈建议使用小型端口驱动程序编写器来实现所有此类通信。

当视频适配器包含没有 WDM 驱动程序的组件时，这种通信模式也很有用。 例如，视频适配器可能有一个用于将视频图像发送到数字平面面板的子板或电路。 在这种情况下，微型端口驱动程序可以使用 **VideoPortQueryServices** 提供的硬件 I-i c 接口将命令发送到 I i2c 总线上的该线路。

![演示如何通过集成线路 (i2c) 接口与子设备通信的示意图](images/i2cfig1.png)

上图说明了微型端口驱动程序如何可以启动 I i2c 总线上两个硬件设备之间的通信。

若要利用视频端口的 I i2c 例程，微型端口驱动程序必须查询适用于 i2c 接口的视频端口驱动程序。 为此，微型端口驱动程序必须分配 [**视频 \_ 端口 \_ I2C \_ 接口**](/windows-hardware/drivers/ddi/video/ns-video-_video_port_i2c_interface) 结构，并将其 **大小** 和 **版本** 成员 (的前两个成员初始化为适当的值) 。 然后，微型端口驱动程序调用视频端口驱动程序的 [**VideoPortQueryServices**](/windows-hardware/drivers/ddi/video/nf-video-videoportqueryservices) 例程， *将 servicesType* 参数设置为 **VideoPortServicesI2C**，并将 *PINTERFACE* 参数设置为部分初始化的视频 \_ 端口 \_ I2C \_ 接口结构。

如果对 **VideoPortQueryServices** 的调用成功，视频端口驱动程序将填充视频 \_ 端口 I2C 接口结构的剩余成员 \_ \_ ，其中包括四个 I I2c 例程的地址： [**I2CStart**](/windows-hardware/drivers/ddi/video/nc-video-pi2c_start)、 [**I2CStop**](/windows-hardware/drivers/ddi/video/nc-video-pi2c_stop)、 [**I2CRead**](/windows-hardware/drivers/ddi/video/nc-video-pi2c_read)和 [**I2CWrite**](/windows-hardware/drivers/ddi/video/nc-video-pi2c_write)。

*I2CStart* 和 *I2CStop* 分别用于启动与子设备的通信，以及终止与子设备的通信。

*I2CRead* 从子设备读取指定数目的字节; *I2CWrite* 向其写入指定的字节数。

 

