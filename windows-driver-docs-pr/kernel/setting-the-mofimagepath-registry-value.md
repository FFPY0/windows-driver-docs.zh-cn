---
title: 设置 MofImagePath 注册表值
description: 设置 MofImagePath 注册表值
keywords:
- WMI WDK 内核，发布架构
- 发布 WMI 架构 WDK
- 架构发布 WDK WMI
- MOF 文件 WDK WMI
- MofImagePath
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 896a46f24c8a73c209b9bd89d17573ba7e51b89c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837979"
---
# <a name="setting-the-mofimagepath-registry-value"></a>设置 MofImagePath 注册表值





可以通过在单独的文件（如 DLL）中包含已编译的 MOF 资源并在注册表中将 **MofImagePath** 设置为该文件的路径，来发布驱动程序的架构。 可以更新以这种方式发布的架构，而无需重新编译该驱动程序。

在单独的文件中发布驱动程序的架构：

1.  编译 MOF 文件，如 [编译驱动程序的 Mof 文件](compiling-a-driver-s-mof-file.md)中所述。

2.  将已编译的 MOF 文件作为资源包括在文件（如 DLL）中。

3.  在驱动程序的 "服务" 项下添加 **MofImagePath** 注册表值。 例如，以下示例显示了名为 *DriverName* 的驱动程序的注册表值：

    ```cpp
    HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services
        \DriverName
            MofImagePath    "\SystemRoot\System32\Drivers\DriverNameMof.dll"
    ```

可以在驱动程序的 INF 文件中设置此密钥，如下所示：

```cpp
; This is the Services section for the driver
[Driver_service_install_section]
AddReg=Driver_AddReg

; This is the Services AddReg section declared above.
[Driver_AddReg]
HKR,,MofImagePath,,DriverMof.dll 
```

有关详细信息，请参阅 [**Inf DDInstall 部分**](../install/inf-ddinstall-services-section.md) 和 [**inf AddReg 指令**](../install/inf-addreg-directive.md) 。

 

