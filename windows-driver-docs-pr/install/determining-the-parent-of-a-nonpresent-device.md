---
title: 确定虚幻设备的父设备
description: 确定虚幻设备的父设备
keywords:
- Setupapi.log 函数 WDK，确定父项
- nonpresent 设备 WDK
- 确定 WDK Setupapi.log 的父设备
- 设备父 WDK
- 父子关系 WDK
- 保存父子关系
- 检索父子关系
- 连接的上级 WDK 的序列
- 祖先 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3222104b7c0f069098727405ab2a9a41645814c4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782891"
---
# <a name="determining-the-parent-of-a-nonpresent-device"></a>确定虚幻设备的父设备





你可以使用本部分中所述的方法来确定 *nonpresent 设备* 的父项，仅当 nonpresent 设备与其父级之间的关系是固定的。  (如果 nonpresent 设备与其父级之间的关系未固定，则不能使用此方法，因为 nonpresent 设备没有特定的父) 。

例如，此方法适用于具有一个或多个接口的 USB 复合设备（如多功能打印机），其中每个接口都表示为子设备。 由于所有子接口设备都依赖于特定复合设备是否为其父设备，因此该设备与其父级之间的关系是固定的。

以下主题介绍了此方法：

[正在保存父/子关系](#saving-the-parent-child-relationship)

[检索父/子关系](#retrieving-the-parent-child-relationship)

[处理 Nonpresent 设备的上级链](#handling-a-chain-of-ancestors-for-a-nonpresent-device)

### <a name="saving-the-parentchild-relationship"></a><a href="" id="saving-the-parent-child-relationship"></a> 正在保存父/子关系

若要保存设备的父/子关系，请提供 *设备共同安装程序* ，将设备的父级的设备实例 ID 保存在设备的硬件注册表项下的用户创建的条目值中。 应使用设备实例 ID，因为它在系统重启和系统进程之间保持不变，而设备实例句柄不会。 当你在共同安装程序中处理 [**DIF_INSTALLDEVICE**](./dif-installdevice.md) 请求时，请按照以下步骤保存设备实例 ID。

**_<em>将直接父项的设备实例 ID 保存到注册表中</em>_*

1.  调用 [_ *CM_Get_Parent* *](/windows/win32/api/cfgmgr32/nf-cfgmgr32-cm_get_parent)获取设备父设备的设备实例句柄。

2.  使用父设备的设备实例句柄，调用 [**CM_Get_Device_ID**](/windows/win32/api/cfgmgr32/nf-cfgmgr32-cm_get_device_idw) 获取父设备的设备实例 ID。

3.  通过使用 DIREG_DEV 标志来调用 [**SetupDiOpenDevRegKey**](/windows/win32/api/setupapi/nf-setupapi-setupdiopendevregkey) ，以获取设备的硬件注册表项的句柄。

4.  调用 **RegSetValueEx** ，将父设备的设备实例 ID 保存在设备的硬件注册表项下的用户创建的条目值中。

### <a name="retrieving-the-parentchild-relationship"></a><a href="" id="retrieving-the-parent-child-relationship"></a> 检索父/子关系

设备共同安装程序将父设备的设备实例 ID 保存在设备硬件注册表项下的条目值中后，你可以检索设备实例 ID。

**_<em>从注册表检索父项的设备实例 ID</em>_* _

1.  调用 _ *SetupDiOpenDevRegKey**，使用 DIREG_DEV 标志获取设备的硬件注册表项的句柄。

2.  调用 **RegQueryValueEx** ，以检索在设备共同安装程序中设置的输入值中保存的父设备的设备实例 ID。

检索父设备的设备实例 ID 后，调用 [**SetupDiOpenDeviceInfo**](/windows/win32/api/setupapi/nf-setupapi-setupdiopendeviceinfoa) 来获取父设备的 [**SP_DEVINFO_DATA**](/windows/win32/api/setupapi/ns-setupapi-sp_devinfo_data) 结构。

### <a name="handling-a-chain-of-ancestors-for-a-nonpresent-device"></a><a href="" id="handling-a-chain-of-ancestors-for-a-nonpresent-device"></a> 处理 Nonpresent 设备的上级链

如果需要给定设备的连接的祖先序列的设备实例 id，则应以可检索它们的方式为注册表中的每个祖先保存设备实例 ID。 请注意，这仅在设备与所有上级之间的关系固定时才有效。

执行此操作的一种方法是，设备共同安装程序使用 **CM_Get_Parent** 获取所有祖先的所有设备实例 id，并将每个实例 id 保存在设备硬件注册表项下的不同条目值中。 您可以使用 [保存父/子关系](#saving-the-parent-child-relationship) 中所述的方法保存每个祖先的设备实例 ID。 然后，您可以按照 [检索父/子关系](#retrieving-the-parent-child-relationship)中所述的相同方式检索每个设备实例 ID。

 

