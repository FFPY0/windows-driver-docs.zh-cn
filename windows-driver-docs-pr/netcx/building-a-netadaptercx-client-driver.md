---
title: 生成 NetAdapterCx 客户端驱动程序
description: 生成 NetAdapterCx 客户端驱动程序
keywords:
- 构建 NetAdapterCx 客户端驱动程序，构建 NIC 驱动程序
ms.date: 06/05/2017
ms.localizationpriority: medium
ms.openlocfilehash: c9ea6236604c29aa8a1a42feb69d8ac90ffa0423
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838765"
---
# <a name="building-a-netadaptercx-client-driver"></a>生成 NetAdapterCx 客户端驱动程序

若要获取最新版本的 Visual Studio 和 Windows 驱动程序工具包 (WDK) ，请访问 [硬件开发人员中心](../download-the-wdk.md)。

使用以下步骤在 Visual Studio 中创建新的 Get-netadapter 客户端驱动程序：

1. 打开 Microsoft Visual Studio。 在 "文件" 菜单上，选择 " **新建 > 项目**"。
2. 在 " **新项目 > 模板" > Visual C++ > Windows Driver > WDF** "对话框中，选择" **内核模式驱动程序 (KMDF) 模板**"。
3. 若要打开 "驱动程序属性页" 对话框，请选择 " **项目 > 属性**"。
4. 在 " **配置属性 > 驱动程序设置" > 网络适配器驱动程序** "对话框中，选择 **指向网络适配器类扩展** 下拉列表的链接，并将其设置为 **" 是 "**。
5. 在 " **配置属性 > 驱动程序设置" > 网络适配器驱动程序** "对话框中，选择" **网络适配器主要版本** 和 **网络适配器次要版本**"。
    1. NetAdapterCx 的当前版本为 **2.0**。 有关详细信息，请参阅 [NetAdapterCx 版本概述](netadaptercx-version-overview.md)。
6. 将以下标头添加到 (的每个源文件，或添加到公共/预编译标头) ：

```C++
#include <ntddk.h>
#include <wdf.h>
#include <netadaptercx.h>
```

若要观看演示如何在 Visual Studio 中创建新的 Get-netadapter 客户端驱动程序的视频，请参阅第9频道上的 [网络适配器类扩展：首个驱动程序](https://aka.ms/netadapter/video2) 视频。
