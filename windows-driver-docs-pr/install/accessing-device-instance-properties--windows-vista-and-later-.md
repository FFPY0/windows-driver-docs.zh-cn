---
title: 访问设备实例属性
description: 访问设备实例属性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c5cb86e7e49e318fe99f99269e8e07a59563c50
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826265"
---
# <a name="accessing-device-instance-properties"></a>访问设备实例属性


在 Windows Vista 和更高版本的 Windows 中，应用程序和安装程序可以通过调用以下 Setupapi.log 函数来访问 [设备实例属性](/previous-versions/ff541334(v=vs.85)) ：

-   [**SetupDiGetDevicePropertyKeys**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdevicepropertykeys)

    **SetupDiGetDevicePropertyKeys** 函数检索设备属性键的数组，这些键标识当前为设备实例设置的设备属性。 有关如何确定为设备设置的属性的信息，请参阅 [确定为设备实例设置的属性](determining-which-properties-are-set-for-a-device-instance.md)。

-   [**SetupDiGetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

    **SetupDiGetDeviceProperty** 函数 [检索为设备实例设置的设备属性](retrieving-a-device-instance-property-value.md)。

-   [**SetupDiSetDeviceProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdisetdevicepropertyw)

    **SetupDiSetDeviceProperty** 函数 [为设备实例设置设备属性](setting-a-device-instance-property-value.md)。

有关如何在 Windows Server 2003、Windows XP 和 Windows 2000 上访问设备属性的信息，请参阅 [使用 setupapi.log 和 Configuration Manager 访问设备属性](using-setupapi-and-configuration-manager-to-access-device-properties.md)。

 

