---
title: 控件面板向导替换
description: 控件面板向导替换
ms.date: 06/09/2020
ms.localizationpriority: medium
ms.openlocfilehash: 3ddb6ca58085e55d86d7f9885a53c008cf3abbc0
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792903"
---
# <a name="control-panel-wizard-replacement"></a>控件面板向导替换

当 "控制面板" 的 "扫描仪和照相机")  (的驱动程序图标时，将显示默认的 UI 扫描器和照相机向导，而不是供应商 UI。

此向导无法使用与通用对话框相同的机制进行替换。 可以从 "控制面板" 中显示供应商 UI。

若要从 "控制面板" 显示你的供应商 UI，你将需要：

- 将获取应用程序注册为此设备的默认永久事件处理程序。

- 编写自定义向导。

自定义向导与使用 [**IWiaUIExtension：:D evicedialog**](/previous-versions/windows/hardware/drivers/ff545069(v=vs.85)) 接口替换的对话框之间没有关系。

请注意，"控制面板" 中的图标始终默认为 Windows Me 和 Windows XP 中的向导。

用户必须右键单击并选择 "显式扫描"，以显示默认的 WIA \_ 事件 \_ 扫描 \_ 图像事件处理程序。

在我的电脑中，相反的情况是，您选择的任何默认处理程序将是用户双击设备图标时使用的处理程序。
