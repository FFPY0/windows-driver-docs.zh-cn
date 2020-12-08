---
title: Windows Me 和 Windows XP 的 WIA 驱动程序错误报告
description: Windows Me 和 Windows XP 的 WIA 驱动程序错误报告
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b3073fd9e3a12082b916a528a143fe3bdee5d144
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818925"
---
# <a name="wia-driver-error-reporting-for-windows-me-and-windows-xp"></a>Windows Me 和 Windows XP 的 WIA 驱动程序错误报告

WIA 微型驱动程序能够以字符串形式向 WIA 应用程序报告扩展的错误信息。 接收到 HRESULT 错误代码后，WIA 应用程序可以调用 **IWiaItemExtras：： GetExtendedErrorInfo** 方法) Microsoft Windows SDK (说明错误的详细信息的用户可读字符串。 此方法报告的字符串应本地化为多种语言。

WIA 微型驱动程序应实现以下方法来执行错误报告：

[**IStiUSD：： GetLastError**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getlasterror) − WIA 服务调用此方法来检索设备特定的错误代码，以获得最近的失败操作。

[**IStiUSD：： GetLastErrorInfo**](/windows-hardware/drivers/ddi/stiusd/nf-stiusd-istiusd-getlasterrorinfo) − WIA 服务调用此方法来检索有关从 **IStiUSD：： GetLastError** 方法调用返回的错误代码的扩展信息。

[**IWiaMiniDrv：:D rvgetdeviceerrorstr**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvgetdeviceerrorstr) − WIA 服务调用此方法来检索任何详细描述错误的可显示字符串，或在出现错误后如何继续操作的说明。 **IWiaItemExtras：： GetExtendedErrorInfo** 方法返回此方法检索到的错误字符串。

如果任何 [IWIAMINIDRV COM 接口](iwiaminidrv-com-interface.md) 方法失败，WIA 服务将请求提供错误信息。
