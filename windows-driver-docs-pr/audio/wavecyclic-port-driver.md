---
title: WaveCyclic 端口驱动程序
description: WaveCyclic 端口驱动程序
keywords:
- WaveCyclic 端口驱动程序 WDK 音频
- PortCls WDK 音频，端口驱动程序
- 音频微型端口驱动程序 WDK，端口驱动程序
- 微型端口驱动程序 WDK 音频、端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66763c68f4caaf3443994c81d4639d391fd4231a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798797"
---
# <a name="wavecyclic-port-driver"></a>WaveCyclic 端口驱动程序


## <span id="wavecyclic_port_driver"></span><span id="WAVECYCLIC_PORT_DRIVER"></span>

**重要提示**  不再建议使用 WaveCyclic，而是改用 WaverRT。


WaveCyclic 端口驱动程序通过基于 DMA 的音频设备来管理波形流的播放或录制，该音频设备处理循环缓冲区中的音频数据。 此设备是音频适配器上的硬件功能。 通常，适配器是主板上的集成芯片组的一部分，或者安装在插入到主板上 PCI 或 ISA 插槽的音频卡上。 适配器驱动程序提供了相应的 [WaveCyclic 微型端口驱动](wavecyclic-miniport-driver.md) 程序对象，该对象绑定到 WaveCyclic 端口驱动程序对象，以形成可捕获或呈现波形流的 [波形筛选器](wave-filters.md) 。

WaveCyclic 端口驱动程序向微型端口驱动程序公开 [IPortWaveCyclic](/windows-hardware/drivers/ddi/portcls/nn-portcls-iportwavecyclic) 接口。 IPortWaveCyclic 继承基接口 [IPort](/windows-hardware/drivers/ddi/portcls/nn-portcls-iport)中的方法。 IPortWaveCyclic 提供了以下附加方法：

[**IPortWaveCyclic::NewMasterDmaChannel**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavecyclic-newmasterdmachannel)

使用内置 DMA 控制器为音频设备创建一个新的主 DMA 通道对象。

[**IPortWaveCyclic::NewSlaveDmaChannel**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavecyclic-newslavedmachannel)

为没有内置 DMA 控制器的音频设备创建一个新的从属 DMA 通道对象。

[**IPortWaveCyclic：： Notify**](/windows-hardware/drivers/ddi/portcls/nf-portcls-iportwavecyclic-notify)

通知端口驱动程序 DMA 控制器已前进到音频流中的新位置。

WaveCyclic 端口和微型端口驱动程序对象通过其各自的 [IPortWaveCyclic](/windows-hardware/drivers/ddi/portcls/nn-portcls-iportwavecyclic) 和 [IMiniportWaveCyclic](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavecyclic) 接口相互通信。 此外，端口驱动程序通过其 [IMiniportWaveCyclicStream](/windows-hardware/drivers/ddi/portcls/nn-portcls-iminiportwavecyclicstream) 接口与微型端口驱动程序的流对象通信。
