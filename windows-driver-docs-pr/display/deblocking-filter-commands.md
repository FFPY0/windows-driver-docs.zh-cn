---
title: 除块筛选器命令
description: 除块筛选器命令
keywords:
- macroblocks WDK DirectX VA，deblocking 筛选器命令
- deblocking 筛选器命令 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 60d6f57bfab85b7638d367eeb75e236c1b1e6107
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808461"
---
# <a name="deblocking-filter-commands"></a>除块筛选器命令


## <span id="ddk_deblocking_filter_commands_gg"></span><span id="DDK_DEBLOCKING_FILTER_COMMANDS_GG"></span>


宏块的 deblocking 筛选器命令可能需要加速器读取当前宏块内和下重构的样本的值。 已构造的值读取是两行以上的示例行：当前宏块以上的两行示例，当前宏块的左侧示例列和当前宏块中的示例。 Deblocking 筛选器命令可能会导致在当前的宏块和当前宏块中的一个样本列（最多三行和三列示例）中修改一个以上的样本行。 因此，对于给定的宏块，deblocking 筛选过程需要之前的两个 macroblocks 的再构造。

下面是两种不同类型的 deblocking 筛选器命令缓冲区：

-   如果 [**DXVA \_ PictureParameters**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)结构的 **bPicDeblockConfined** 成员为零) ，则需要访问和修改当前 deblocking 筛选器命令缓冲区 (以外的 macroblocks 的值。

-   当 **bPicDeblockConfined** 为 1) 时，不需要访问和修改当前 deblocking 筛选器命令缓冲区 (以外的 macroblocks 的值。

若要处理第一种类型的 deblocking 命令缓冲区，加速器必须确保对影响当前缓冲区中控制的 macroblocks 的 macroblocks 的所有缓冲区完成宏块重构。 必须在处理当前缓冲区中的 deblocking 命令之前完成此操作。

若要处理第二种类型的 deblocking 命令缓冲区，加速器只使用当前缓冲区中以前的重构值。

可以通过以下两种方式之一在加速器中执行 deblocking 筛选器操作：

-   首先对整个缓冲区或帧的运动预测和残留差异数据进行处理，然后通读其中一些示例的值，并在 deblocking 筛选器操作的结果中修改它们。

-   使用残留差异数据缓冲区以协调方式处理 deblocking 命令缓冲区。 在这种情况下，将在向目标图片图面写入重构的输出值之前处理 deblocking 命令缓冲区。

**注意**   Deblocked 图片的目标图片表面可能不同于在 deblocking 之前重建图片的位置。 然后，这将支持 "在循环外" deblocking 作为 postdecoding 进程，该进程不影响用于预测下一个图片的示例值。

 

 

