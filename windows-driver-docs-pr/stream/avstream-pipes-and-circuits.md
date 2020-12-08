---
title: AVStream 管道和线路
description: AVStream 管道和线路
keywords:
- AVStream 分配器 WDK
- 分配器 WDK AVStream
- 用户模式源 WDK AVStream
- 帧 WDK AVStream
- 转换筛选器 WDK AVStream
- 管道 WDK AVStream
- AVStream 管道 WDK
- 共享分配器 WDK AVStream
- 就地转换筛选器 WDK AVStream
- 源筛选器 WDK AVStream
- 呈现器筛选 WDK AVStream
- 非就地转换筛选 WDK AVStream
- 线路 WDK AVStream
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4fc363bedac12aac9bf8e2b34ea8ee3845363b7c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792115"
---
# <a name="avstream-pipes-and-circuits"></a>AVStream 管道和线路





*管道* 是一组共享公共 [分配](avstream-allocators.md)器的 AVStream 筛选器。

下图显示了由三个 AVStream 筛选器组成的管道：源筛选器、 *就地* 转换筛选器和呈现器筛选器。

![使用所有 avstream 筛选器阐释管道的关系图](images/pipe1.png)

在此示例中， [KSProxy](/windows-hardware/drivers/ddi/_stream/index) (未显示) 选择了分配器，由关系图中的 **分配** 块表示。

AVStream 创建与源筛选器相关联的内部请求方对象。 在关系图中，请求者显示为 " **必需**"。微型驱动程序在 KSPIN 描述符的 **AllocatorFraming** 成员（ [**\_ \_ 例如**](/windows-hardware/drivers/ddi/ks/ns-ks-_kspin_descriptor_ex) ，要分配给帧的内存类型和连续内存量）中指定。 相应地，请求者从分配器获取帧，并将其传递到线路中的下一个组件。

源筛选器中的数据流入其他 AVStream 驱动程序实现的转换筛选器。

最后，数据流入第三个 AVStream 筛选器实现的呈现器筛选器。

由于此图中的所有 pin 都是 AVStream 的 pin，AVStream 使用其自己的内部传输接口，而不是通过 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)发送 irp，从而减少延迟并提高性能。

具体而言，当应用程序使图形转换到 [**KSSTATE \_ 获取**](/windows-hardware/drivers/ddi/ks/ne-ks-ksstate) (时，当用户在 GraphEdit) 中单击 " **播放** " 时，AVStream 直接连接筛选器队列，如上所示。

因此，向后发送的帧将返回到请求者，在呈现完成后可以回收这些帧。 此 AVStream 数据路径是一条 *线路*。

请考虑下图所示的第二个示例，其中，转换筛选器不是 AVStream 筛选器，但仍是内核模式筛选器。

![使用非 avstream 内核模式转换筛选器说明管道的关系图](images/pipe2.png)

如第一个示例中所示，此示例包含三个筛选器： AVStream 源、KS 转换 (这可能是直接使用 KS 的驱动程序，或者是 stream 类) 下的微型驱动程序，以及 AVStream 呈现器。

如第一个插图中所示，pin 是第一次互连的。 但是，当筛选器关系图转换为 **KSSTATE \_** 时，内核流1.0 筛选器不支持 AVStream 传输接口。 因此，AVStream 不会绕过 pin;相反，它必须使用 i/o 在筛选器之间移动数据。

具体而言，当框架离开源筛选器的队列时，AVStream 会调用 [**IoCallDriver**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocalldriver)。 在此调用中， *Irp* 参数包含要从源的输出插针传递到转换筛选器的帧。

呈现器的输入插针收到 IRP 后，该 pin 会将 IRP 置于队列中。 呈现器驱动程序完成帧后，会将帧返回到呈现器的输入插针，如第二个示例中所示。

AVStream 现在调用 [**IoCompleteRequest**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iocompleterequest) 以返回上游帧。 源筛选器的输出插针接收到完成通知。 然后，微型驱动程序的 [*pin 进程回调*](/windows-hardware/drivers/ddi/ks/nc-ks-pfnkspin) 例程可以调用 [**KsStreamPointerUnlock**](/windows-hardware/drivers/ddi/ks/nf-ks-ksstreampointerunlock) ，并将帧移回要回收到线路中的请求者。

假设帧源处于用户模式的最终示例。  (或者，最终帧目标可能处于用户模式。 ) 

在下图中，内核模式 *非就地* 转换筛选器接收来自用户模式 DirectShow 筛选器的帧，并将转换后的帧发送到内核模式 AVStream 呈现器：

![阐释从用户模式源接收并发送到 avstream 呈现器的帧的关系图](images/pipe3.png)

当帧从用户模式到达时，AVStream 固定对象会将其放在输入管道部分的队列中。

非就地转换筛选器以内核模式分配转换后的帧，然后使用第二个管道作为这些帧的线路。 由于呈现器是一个 AVStream 筛选器，因此 AVStream 将绕过 pin，并使用 AVStream 传输接口将帧直接置于呈现筛选器的队列中。

微型驱动程序可以通过调用 [**KsPinSubmitFrame**](/windows-hardware/drivers/ddi/ks/nf-ks-kspinsubmitframe)或 [**KsPinSubmitFrameMdl**](/windows-hardware/drivers/ddi/ks/nf-ks-kspinsubmitframemdl)将 [帧注入](frame-injection.md)到线路。 如果微型驱动程序使用此方法，则 AVStream 请求方将接收这些调用的结果而不是来自内核模式分配器的帧。

 

