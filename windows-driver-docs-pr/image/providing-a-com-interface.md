---
title: 提供 COM 接口
description: 提供 COM 接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0f702877be339e252c7d911b828db195c2085538
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829627"
---
# <a name="providing-a-com-interface"></a>提供 COM 接口





WIA 微型驱动程序必须支持 WIA 服务识别和加载的 **IWiaMiniDrv**、 **IStiUSD** 和 **IUnknown** 接口。 以下接口标识符应添加到 WIA 驱动程序的 **QueryInterface** 方法中：

-   **IID \_IWiaMiniDrv** - [IWiaMiniDrv 接口](/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv)的接口标识符，它是用于访问 WIA 特定功能的标准 WIA 接口。

-   **IID \_IStiUSD** - [IStiUSD 接口](/windows-hardware/drivers/ddi/_image/index)的接口标识符，一种标准的 STI 接口，用于访问 WIA 驱动程序的 STI 功能

-   **IID \_IUnknown** - **iunknown** 接口的接口标识符，它是在 Microsoft Windows SDK 文档中定义的标准 COM 接口。

微型驱动程序将导出这些接口标识符，以响应调用微型驱动程序的 **QueryInterface** 方法的 WIA 服务。

有关如何实现这些接口的示例，请参阅 *wiascanr* scanner 示例微型驱动程序 files *wiascanr*、 *iwiaminidrv* 和 *istiusd 或 s* Ee *wiacam* 相机示例微型驱动程序 files *iwiaminidrv* 和 *istiusd*。

 

