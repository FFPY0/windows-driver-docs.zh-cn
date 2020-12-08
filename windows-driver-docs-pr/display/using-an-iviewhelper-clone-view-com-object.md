---
title: 使用 IViewHelper Clone-View COM 对象
description: 使用 IViewHelper Clone-View COM 对象
keywords:
- TMM WDK 显示，关于 IViewHelper
- 监视器配置 WDK 显示，关于 IViewHelper
- 监视配置 WDK 显示，检测新监视器
- 监视配置 WDK 显示，持久化
- 视频显示网络 WDK 显示，关于 IViewHelper
- VidPN WDK 显示，关于 IViewHelper
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: df38af586e15bb37a163a9ce1755c1f2fada6a59
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826581"
---
# <a name="using-an-iviewhelper-clone-view-com-object"></a>使用 IViewHelper Clone-View COM 对象


TMM 将使用新监视器中的硬件供应商克隆查看 [IViewHelper](/windows-hardware/drivers/ddi/index) COM 接口对象的方法，并保留监视器配置。 在保留的监视器配置中，TMM 将 (的显示数据（即显示模式和拓扑数据）还原为监视) 。 TMM 可以通过 [**IViewHelper：： SetConfiguration**](/previous-versions/windows/hardware/drivers/ff568176(v=vs.85)) 方法将此显示数据传递给用户模式显示驱动程序，以便驱动程序可以修改或折叠其他显示数据 (例如，伽玛或电视设置) 。

[视频显示网络中的错误 (VidPN) ](multiple-monitors-and-video-present-networks.md)通过[IViewHelper](/windows-hardware/drivers/ddi/index)的方法返回。 因此，如果 TMM 应用不正确的拓扑，则 VidPN 将失败，并且失败结果会传递回调用函数。 将目标映射到两个源或使用 VidPN 无法识别的目标或源标识符就是不正确的拓扑示例。

TMM 通过 **UserModeDriverGUID** string 注册表值确定 [IViewHelper](/windows-hardware/drivers/ddi/index) COM 接口对象。 硬件供应商应该在显示设备结构的 **DeviceKey** 成员指定的注册表项下添加此值 \_ 。 对 Win32 **EnumDisplayDevices** 函数的调用将在显示设备中返回 \_ *lpDisplayDevice* 参数指向的注册表项信息。 如果存在多个 **DeviceKey** 名称，则此值应显示在每个键下。 下面是设备密钥和 **UserModeDriverGUID** 字符串注册表值的示例：

```registry
[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Video\{7661971C-A9BD-48B5-ACBC-298A8826535D}\0000]
"UserModeDriverGUID"="{YYYYYYYY-YYYY-YYYY-YYYY-YYYYYYYYYYYY}"
```

要使 COM 加载 [IViewHelper](/windows-hardware/drivers/ddi/index) com 接口对象，应将 COM 对象注册为进程内 (进程内) 处理程序，并且线程模型应同时为两者。 已注册的 GUID 应该与 **UserModeDriverGUID** 中的 guid 匹配。 有关这两个线程模型属性的信息，请参阅 Microsoft Windows SDK 文档。

只应复制并注册系统目录中的 [IViewHelper](/windows-hardware/drivers/ddi/index) COM 接口对象 dll 的正确编译版本。 也就是说，只应为64位操作系统复制和注册64位 **IViewHelper** dll，为32位操作系统复制并注册32位 **IViewHelper** dll。 两个 DLL 二进制文件不应同时出现在同一台计算机上。 如果两个二进制文件同时存在于同一台计算机上，即使 windows on windows (WOW) ，TMM 也不会正常运行。

 

