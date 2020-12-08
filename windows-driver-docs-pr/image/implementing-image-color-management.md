---
title: 实现图像颜色管理
description: 实现图像颜色管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9850c727133dbbfb4ddb7519d86e92c9a180690b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793699"
---
# <a name="implementing-image-color-management"></a>实现图像颜色管理





WIA 依赖于 Microsoft Windows 中提供的 "图像颜色管理" (ICM) 系统。 Microsoft Windows SDK 文档中介绍了 ICM。

为了获得最佳的应用程序兼容性，所有微型驱动程序都应在 sRGB 颜色空间中返回数据。 如果设备本身在不同的颜色空间中生成数据，则微型驱动程序应使用 ICM 函数将其输出映射到 sRGB。 某些应用程序会实现 ICM，并可能希望检索本机颜色空间中的数据。 微型驱动程序可通过以下方式实现此功能：在安装信息 (INF) 文件中指定本机颜色空间，并为 [**WIA \_ IPA \_ 应用 \_ 颜色 \_ 映射**](./wia-ipa-app-color-mapping.md) 属性指定有效的值1。

当应用程序将属性设置为1时，微型驱动程序应停止映射到 sRGB，并允许应用程序处理映射。 应用程序使用 [**WIA \_ IPA \_ ICM \_ PROFILE \_ NAME**](./wia-ipa-icm-profile-name.md) 属性的当前值作为设备中的数据配置文件。 用户使用系统对话框设置属性，并且微型驱动程序不应更改该属性。

 

