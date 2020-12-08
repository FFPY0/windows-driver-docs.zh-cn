---
title: Direct3D 着色器代码
description: Direct3D 着色器代码
ms.date: 01/05/2018
ms.localizationpriority: medium
ms.openlocfilehash: ce435a920fb0c2e70aa660e57e6ae9fb6066537f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809457"
---
# <a name="direct3d-shader-codes"></a>Direct3D 着色器代码


像素着色器代码遵循 \_ 命令流中的 D3DHAL DP2CREATEPIXELSHADER 结构。 对于 DirectX 8.1 及更早版本，顶点着色器代码遵循 D3DHAL \_ DP2CREATEVERTEXSHADER 结构。 对于 DirectX 9.0 和更高版本，顶点着色器代码遵循 D3DHAL \_ DP2CREATEVERTEXSHADERFUNC 结构。 运行时在调用驱动程序的 D3dDrawPrimitives2 函数时，将创建像素或顶点着色器。 若要创建像素着色器，运行时将使用 D3DDP2OP \_ CREATEPIXELSHADER 操作代码调用 D3dDrawPrimitives2。 若要在 DirectX 8.1 和更早版本中创建顶点着色器，运行时将使用 D3DDP2OP \_ CREATEVERTEXSHADER 操作代码调用 D3dDrawPrimitives2。 若要在 DirectX 9.0 和更高版本中创建顶点着色器，运行时将使用 D3DDP2OP \_ CREATEVERTEXSHADERFUNC 操作代码调用 D3dDrawPrimitives2。

本节介绍单个着色器代码的格式和组成每个着色器代码的标记。

[着色器代码格式](shader-code-format.md)

[着色器代码标记](shader-code-tokens.md)

[着色器操作代码](/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3dshader_instruction_opcode_type)

[着色器寄存器类型](/windows-hardware/drivers/ddi/d3d9types/ne-d3d9types-_d3dshader_param_register_type)

[着色器相对寻址](shader-relative-addressing.md)

 

