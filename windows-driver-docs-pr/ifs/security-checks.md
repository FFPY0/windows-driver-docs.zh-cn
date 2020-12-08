---
title: 文件系统中的安全检查
description: 安全检查
keywords:
- 安全 WDK 文件系统，安全检查
- 安全检查 WDK 文件系统
- 安全检查 WDK 文件系统，有关安全检查
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 22d3ade64426b0a7807451aacd8f7e6e6a48e4b7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96789945"
---
# <a name="security-checks-in-file-systems"></a>文件系统中的安全检查

文件系统对安全性的责任是在安全检查领域。 它们是在文件系统内实现的，因为它是实际 "拥有" 对象的窗口的一部分。 安全实现的目标是将由文件系统实现的策略 () ，以保护其对象，并将安全引用) 监视器实现的机制 (实现访问决策。

换句话说，文件系统开发人员负责在适当的时间调用安全引用监视器来验证对文件系统资源的正确访问权限。 文件系统不需要了解有关安全引用监视器如何做出这些安全决策的详细信息。 本部分介绍文件系统可能会考虑添加安全检查的要点。

本节包括下列主题：

[应用设备对象上的安全描述符](applying-security-descriptors-on-the-device-object.md)

[IRP_MJ_CREATE 上的安全检查](irp-mj-create-dispatch-routine.md)

[IRP_MJ_QUERY_SECURITY 和 IRP_MJ_SET_SECURITY 上的安全检查](irp-mj-query-security-and-irp-mj-set-security.md)

[IRP_MJ_DIRECTORY_CONTROL 上的安全检查](irp-mj-directory-control2.md)

[IRP_MJ_FILE_SYSTEM_CONTROL 上的安全检查](./irp-mj-file-system-control.md)

[IRP_MJ_SET_INFORMATION 上的安全检查](./irp-mj-set-information.md)

[模拟](impersonation.md)

[进程和线程终止问题](process-and-thread-termination-issues.md)
