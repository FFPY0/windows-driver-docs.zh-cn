---
title: '设备属性页提供程序的要求 (共同安装程序) '
description: 设备属性页提供程序（辅助安装程序）的特定要求
keywords:
- 设备属性页 WDK 设备安装，DIF_ADDPROPERTYPAGE_ADVANCED
- 属性页 WDK 设备安装，DIF_ADDPROPERTYPAGE_ADVANCED
- 自定义属性页 WDK 设备安装，DIF_ADDPROPERTYPAGE_ADVANCED
- DIF_ADDPROPERTYPAGE_ADVANCED
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da06ed7c9cb187945f02cd2c0a87006b2c493939
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820707"
---
# <a name="specific-requirements-for-device-property-page-providers-co-installers"></a>设备属性页提供程序（辅助安装程序）的特定要求





提供一个或多个自定义设备属性页的 [共同安装程序](writing-a-co-installer.md) 必须处理 [**DIF_ADDPROPERTYPAGE_ADVANCED**](./dif-addpropertypage-advanced.md) 设备安装函数 (DIF) 代码。 当用户在 "设备管理器" 或 "控制面板" 中单击设备的 " **属性** " 选项卡时，设备管理器发出此请求。

作为对此请求的响应，安装程序提供有关其每个自定义属性页的信息，创建页面，并将创建的页添加到设备的动态属性页列表中。 安装程序通过初始化并返回请求的类安装参数的 SP_ADDPROPERTYPAGE_DATA 结构来实现此功能。

如果用户更改了任何属性，则在安装程序通过调用 [**SetupDiSetDeviceInstallParams**](/windows/win32/api/setupapi/nf-setupapi-setupdisetdeviceinstallparamsa)设置新参数之后设备管理器向安装程序发送 [**DIF_PROPERTYCHANGE**](./dif-propertychange.md)的 DIF 代码。

有关如何通过 [共同安装程序](writing-a-co-installer.md)创建自定义设备属性页的详细信息，请参阅 [设备属性页提供程序的一般要求](general-requirements-for-device-property-page-providers.md)。

 

