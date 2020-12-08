---
title: 访问自定义设备属性
description: 访问自定义设备属性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3d224cde14c781e0982288c00f0a4d3635f7157d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826279"
---
# <a name="accessing-custom-device-properties"></a>访问自定义设备属性


在 Windows Vista 和更高版本的 Windows 中， [统一设备属性模型](unified-device-property-model--windows-vista-and-later-.md) 支持使用 [属性键](property-keys.md) 创建和访问自定义设备属性。 有关详细信息，请参阅 [创建自定义设备属性](creating-custom-device-properties.md)。

在 Windows Server 2003、Windows XP 和 Windows 2000 上，可以在系统提供的与设备相关的组件的注册表项下创建自定义注册表项值。 下面的列表包含要为每种类型的设备组件调用以打开相应系统提供的注册表项的 Setupapi.log 函数。 打开系统定义的注册表项后，应用程序和安装程序可以调用基于 Windows 的注册表函数，以修改打开的注册表项下的自定义注册表项值。

-   设备实例硬件属性的自定义注册表项值应位于设备实例的硬件注册表项下。 调用 [**SetupDiOpenDevRegKey**](/windows/win32/api/setupapi/nf-setupapi-setupdiopendevregkey) 并在 *Flags* 参数中提供 DIREG_DEV，以检索设备实例的硬件密钥的句柄。 可以通过调用 [**SetupDiGetCustomDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetcustomdevicepropertya) 函数来检索在设备实例的硬件注册表项下设置的自定义注册表项值。

-   设备实例软件属性的自定义注册表项值应位于设备实例的软件注册表项下。 调用 **SetupDiOpenDevRegKey** 并在 *Flags* 参数中提供 DIREG_DRV，以检索设备实例的软件密钥的句柄。

-   [设备安装程序类属性](accessing-device-setup-class-properties.md)的自定义注册表项值应位于设备安装程序类注册表项下。 调用 [**SetupDiOpenClassRegKeyEx**](/windows/win32/api/setupapi/nf-setupapi-setupdiopenclassregkeyexa) 并在 *Flags* 参数中提供 DIOCR_INSTALLER，以检索设备安装程序类的注册表项的句柄。

-   设备接口类属性的自定义注册表项值应位于设备接口类注册表项下。 调用 **SetupDiOpenClassRegKeyEx** 并在 *Flags* 参数中提供 DIOCR_INTERFACE，以检索设备接口类的注册表项的句柄。

-   设备接口属性的自定义注册表项值应位于设备接口注册表项下。 调用 [**SetupDiOpenDeviceInterfaceRegKey**](/windows/win32/api/setupapi/nf-setupapi-setupdiopendeviceinterfaceregkey) 可检索设备接口类的注册表项的句柄。

检索到某个注册表项的句柄之后，在对 [RegQueryValueEx](/windows/win32/api/winreg/nf-winreg-regqueryvalueexa) 或 [RegSetValueEx](/windows/win32/api/winreg/nf-winreg-regsetvalueexa) 的调用中提供该句柄，以便检索或设置与自定义设备属性对应的自定义注册表项值。

在不再需要访问注册表项后，调用 [RegCloseKey](/windows/win32/api/winreg/nf-winreg-regclosekey) 函数关闭该注册表项。

