---
title: 为驱动程序签名以便公开发布
description: 为驱动程序签名以便公开发布
keywords:
- 驱动程序签名 WDK，公共版本
- 对驱动程序进行签名 WDK，公共版本
- 数字签名 WDK，公共版本
- 签名 WDK，公共版本
- 公共版本驱动程序签名 WDK
- 版本签名 WDK
- 公共版本驱动程序签名 WDK，版本签名
- release 签名 WDK，关于发布签名
- 版本签名 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 04d1ea08e1398c162df9fbc8e102a508a71fd9dd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825133"
---
# <a name="signing-drivers-for-public-release"></a>为驱动程序签名以便公开发布


"发布签名" 标识内核模式二进制 (（例如，加载到 Windows Vista 和更高版本的 Windows 中的驱动程序或 *.dll*) 的发布服务器）。 内核模式二进制文件通过以下任一方法进行释放：

-   通过[Windows 徽标计划](/windows-hardware/drivers)获取的[WHQL 版本签名](whql-release-signature.md)。

-   通过软件发行者证书创建的发布签名 [ (SPC) ](software-publisher-certificate.md)。

要了解发布签名 [驱动程序包](driver-packages.md)中涉及的步骤，请查看以下主题：

<a href="" id="introduction-to-release-signing"></a>[发布签名简介](introduction-to-release-signing.md)  
本主题介绍对驱动程序包进行 release 签名的原因，并提供对发布签名过程的高级摘要。

<a href="" id="how-to-release-sign-a-driver-package"></a>[如何 Release-Sign 驱动程序包](how-to-release-sign-a-driver-package.md)  
本主题提供对发布签名过程的高级概述，并通过使用 Windows 驱动程序工具包 (WDK) 中的 *toastpkg.inf* 示例驱动程序包来查看发布签名的许多示例。

有关发布签名过程的详细信息，请参阅以下主题：

[WHQL 发布签名](whql-release-signature.md)

[发布证书](release-certificates.md)

[对驱动程序包进行发布签名](release-signing-driver-packages.md)

 

