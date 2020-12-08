---
title: IRP_MJ_FILE_SYSTEM_CONTROL 上的安全检查
description: 描述文件系统对 IRP_MJ_FILE_SYSTEM_CONTROL 进行安全检查的方式
keywords:
- IRP_MJ_FILE_SYSTEM_CONTROL
- 安全 WDK 文件系统，添加安全检查
- 安全检查 WDK 文件系统，IRP_MJ_FILE_SYSTEM_CONTROL
- 文件系统控制 WDK 安全性
- 设置文件信息处理 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eebb2c479c9fa45753edd669eb67264e71130f16
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798193"
---
# <a name="security-checks-on-irp_mj_file_system_control-ifs"></a>IRP_MJ_FILE_SYSTEM_CONTROL (IFS 的安全检查) 

文件系统控件允许文件系统实质上执行任何专用操作。 现有 Windows 文件系统具有许多专用控件和它们以及为 Windows 开发的任何第三方文件系统，因此必须严格检查所有参数。 此外，FSCTL 操作通常具有受限的安全权限。 在 [FASTFAT 示例代码](/samples/microsoft/windows-driver-samples/fastfat-file-system-driver/) 中可以看到这些代码 (参阅 fsctrl 中的 **FatInvalidateVolumes** 函数，例如) 。 这是权限检查的一个示例。 在这种情况下，FASTFAT 文件系统的策略是要求在系统上启用给定的权限。

如果文件系统已使用 CTL_CODE 宏在文件系统操作定义中设置这些位，则 i/o 管理器将强制执行特定 FSCTL 操作的 FILE_READ_DATA 和 FILE_WRITE_DATA 权限。 必须由文件系统 (FILE_READ_ATTRIBUTES 权限检查所需的所有其他权限，例如) 如果这是文件系统的策略。
