---
title: 使用自定义压缩
description: 使用自定义压缩
keywords:
- 光栅数据压缩 WDK Unidrv
- 压缩光栅数据 WDK Unidrv
- 自定义的光栅数据压缩 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f4233715f6caf998e8f2e79706deff0a90a16571
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835465"
---
# <a name="using-customized-compression"></a>使用自定义压缩





如果要提供自定义的压缩算法，请包含 CmdEnableOEMComp 命令项以指定启用算法的命令。 如果打印机可以禁用压缩，则可以选择包含 CmdDisableCompression 项来指定禁用压缩的命令。 还必须提供实现 [**IPrintOemUni：： Compression**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemuni-compression)方法的 [呈现插件](rendering-plug-ins.md)。

如果提供自定义的压缩算法，还可以使用支持 Unidrv 的算法。 对于每个扫描行，Unidrv 将尝试每个压缩算法，并选择生成最多压缩结果的算法。  (有关 Unidrv 支持的算法的信息，请参阅 [使用 Unidrv-Supported 压缩](using-unidrv-supported-compression.md)。 ) 当 Unidrv 找到最佳算法时，它会压缩扫描行数据。 然后，它会将相应命令条目指定的命令发送到打印机，后跟压缩后的数据。

有关 CmdEnableOEMComp 和 CmdDisableCompression 条目的详细信息，请参阅 [光栅数据压缩命令](raster-data-compression-commands.md)。

有关自定义压缩的详细信息，请参阅 [自定义数据流压缩](customized-data-stream-compression.md)。

 

