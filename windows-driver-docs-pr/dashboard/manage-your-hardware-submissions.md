---
title: 管理硬件提交
description: 为合作伙伴中心管理硬件提交
ms.topic: article
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e217f6a955dd3c75cb9852376fbe2fae6c7933d0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96800331"
---
# <a name="managing-hardware-submissions-in-the-partner-center"></a>在合作伙伴中心内管理硬件提交

提交面向 Windows 10 的 Windows 硬件兼容性计划（或适用于以前版本的 Windows 的认证计划）的产品后，可以通过仪表板管理该产品。

## <a name="find-a-hardware-submission"></a>查找硬件提交

请参阅[查找硬件提交](find-hardware-submission.md)。

## <a name="update-an-hck-or-hlk-hardware-submission-using-the-driver-update-acceptable-dua-process"></a>使用驱动程序更新可接受 (DUA) 过程更新 HCK 或 HLK 硬件提交

> [!Note]
> 只能从初始提交创建 DUA 提交。
> - 因为不能对 DUA 提交执行 DUA，与其他公司共享的 DUA 提交不会显示“下载 DUA Shell”按钮。

有关如何从 DUA Shell 创建 DUA 提交的说明，请参阅[创建仅更新驱动程序的包](/windows-hardware/test/hlk/user/create-a-driver-only-update-package)。

## <a name="registering-an-extensionid"></a>注册 ExtensionId

当你提交要签名的扩展 INF 时，仪表板会检查指定的 **ExtensionId** 是否先前已注册到其他帐户。
如果是，你将看到一条消息，提示你提供不同的 ID。 如果不是，仪表板会将其与你的帐户相关联。

有关指定 **ExtensionId** 的详细信息，请参阅 [使用扩展 INF 文件](../install/using-an-extension-inf-file.md)。

请注意，在你的提交中，你只能使用注册到你的帐户的 ExtensionID。

## <a name="related-topics"></a>相关主题

- [创建新硬件提交](create-a-new-hardware-submission.md)
- [获取由 Microsoft 签名的适用于多个 Windows 版本的驱动程序](get-drivers-signed-by-microsoft-for-multiple-windows-versions.md)
- [驱动程序外部测试](driver-flighting.md)
