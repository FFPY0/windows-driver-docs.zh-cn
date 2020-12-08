---
title: 适合设备和驱动程序制造商的设备管理器
description: 设备管理器提供了解决驱动程序和设备的安装问题的方法。
keywords:
- 设备管理器 WDK
- 设备管理器 WDK，关于设备管理器
ms.date: 10/01/2018
ms.localizationpriority: medium
ms.openlocfilehash: edf7ae69ed6ff61172cfc1cb3b833776e5cd3bae
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839495"
---
# <a name="using-device-manager"></a>使用设备管理器

要开始设备管理器，请在 "文件资源管理器" 中选择并按住 (或右键单击 ") **这台电脑**"，选择 " **管理**"，然后从生成的对话框中列出的系统工具中选择 " **设备管理器** "。

设备管理器显示有关每个设备的信息。 这包括设备类型、设备状态、制造商、设备特定的属性以及有关设备驱动程序的信息。

如果你的设备需要启动计算机，则设备安装的问题可能会阻止计算机启动。 在这些情况下，必须使用内核调试器对设备安装进行故障排除。 有关详细信息，请参阅 [ (内核模式) 入门 ](../debugger/getting-started-with-windbg--kernel-mode-.md)。

如果您的设备不需要启动计算机，设备管理器会在设备管理器对话框中的设备名称旁边放置一个黄色惊叹号。 设备管理器还提供了一个描述该问题的错误消息。 有关错误消息的详细信息，请参阅 [设备管理器错误消息](device-manager-error-messages.md)。

设备管理器可以显示隐藏的设备。 当你测试新的 PnP 设备的安装时，这会很有帮助。 有关详细信息，请参阅 [查看隐藏的设备](viewing-hidden-devices.md)。

设备管理器提供每个设备的 "属性" 对话框中的详细信息。 选择并按住 (或右键单击) 设备名称，然后选择 " **属性**"。 " **常规**"、" **驱动程序**"、" **详细信息**" 和 " **事件** " 选项卡包含调试错误时可能有用的信息。 有关详细信息，请参阅 [设备管理器详细信息 "选项卡](device-manager-details-tab.md)。
