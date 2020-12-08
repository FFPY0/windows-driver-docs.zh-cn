---
title: 扩展的 Blt 标志
description: 扩展的 Blt 标志
keywords:
- 扩展 blt 标志 WDK DirectX 9。0
- DDBLT_EXTENDED_FLAGS
- blt 标志扩展 WDK DirectX 9。0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 47b145e5a91ca54b296c051d22d872190b281566
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838299"
---
# <a name="extended-blt-flags"></a>扩展的 Blt 标志


## <span id="ddk_extended_blt_flags_gg"></span><span id="DDK_EXTENDED_BLT_FLAGS_GG"></span>


DirectX 9.0 使用 DDBLT \_ 扩展 \_ 标志 blt 标志来扩展使用 DDBLT \_ *Xxx* blt 标志，这些标志在 [**DD \_ dwFlags**](/windows/win32/api/ddrawint/ns-ddrawint-dd_bltdata)结构的 **BLTDATA** 成员中可用。 当 DirectX 9.0 运行时调用显示器驱动程序的 [*DdBlt*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_surfcb_blt)函数来执行 blt 操作时，运行时可以 \_ \_ 使用按位 "or" 将 DDBLT 扩展标志与 DdBlt \_ *Xxx* 标志合并，以创建标志的新含义。 然后，该驱动程序将确定 DDBLT \_ 扩展 \_ 标志的状态，重新解释标志的含义，并相应地执行 blt 操作。 驱动程序在 blt 从后台缓冲区到桌面时，使用此机制来确定是否应在线性颜色空间上 [执行伽玛更正](performing-gamma-correction-on-swap-chains.md) 。 驱动程序还使用扩展 blt 标志来确定是否请求了 [stretch array.blit 操作](supporting-stretch-blit-operations.md) 。

 

