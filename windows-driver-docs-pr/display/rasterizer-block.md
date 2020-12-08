---
title: 光栅器块
description: 光栅器块
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: baeca6f6090a9cb90514cafbc477a90f4f4c9fbd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96810095"
---
# <a name="rasterizer-block"></a>光栅器块


光栅器会阻止剪辑，设置基元，并确定如何调用 "像素着色器" 阶段。 Direct3D 运行时不会将光栅化块视为管道中的一个阶段。 相反，Direct3D 运行时将光栅化程序块视为管道阶段之间的接口，以执行一组重大的固定函数操作。 许多这些固定函数操作都可以由软件开发人员进行调整。

光栅化程序始终决定在剪辑空间中提供输入位置，执行剪辑和透视分割，并应用视区比例和偏移量。

Direct3D 运行时调用以下驱动程序函数来创建、设置和销毁光栅化程序的状态：

[**CalcPrivateRasterizerStateSize**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_calcprivaterasterizerstatesize)

[**CreateRasterizerState**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_createrasterizerstate)

[**DestroyRasterizerState**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_destroyrasterizerstate)

[**SetRasterizerState**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setrasterizerstate)

[**SetScissorRects**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setscissorrects)

[**SetViewports**](/windows-hardware/drivers/ddi/d3d10umddi/nc-d3d10umddi-pfnd3d10ddi_setviewports)

 

