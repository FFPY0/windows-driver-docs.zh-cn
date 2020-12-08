---
title: HKLM\SYSTEM\CurrentControlSet\Services 注册表树
description: HKLM\SYSTEM\CurrentControlSet\Services 注册表树存储有关系统上的每个服务的信息。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bbcf020cf7e2d3c906edbe117bf39859e1bf4254
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791741"
---
# <a name="hklmsystemcurrentcontrolsetservices-registry-tree"></a>HKLM \\ SYSTEM \\ CurrentControlSet \\ Services 注册表树





**HKLM \\ system \\ CurrentControlSet \\ Services** 注册表树存储有关系统上的每个服务的信息。 每个驱动程序都有一个格式为 **HKLM \\ SYSTEM \\ CurrentControlSet \\ Services \\**<em>DriverName</em>的键。 PnP 管理器在调用驱动程序的 [**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)例程时，会在 *RegistryPath* 参数中传递该驱动程序的路径。 驱动程序可以将全局驱动程序定义的数据存储在 **服务** 树中其键的 **Parameters** 子项下。 此密钥下存储的信息可在其初始化过程中供驱动程序使用。

以下密钥和值项特别感兴趣：

<a href="" id="imagepath"></a>**ImagePath**  
一个值项，它指定驱动程序的映像文件的完全限定路径。 Windows 使用驱动程序的 INF 文件中的所需 **ServiceBinary** 项来创建此值。 此项位于驱动程序的 [**INF AddService 指令**](inf-addservice-directive.md)引用的 *服务安装部分*。 此路径的典型值为 *% SystemRoot%* \\ *system32 driver \\ \\ DriverName*，其中 *DriverName* 是驱动程序的 **服务** 密钥的名称。

<a href="" id="parameters"></a>**Parameters**  
用于存储特定于驱动程序的数据的键。 对于某些类型的驱动程序，系统需要查找特定的值项。 您可以使用驱动程序的 INF 文件中的 **AddReg** 条目向此子项添加值项。

<a href="" id="performance"></a>**性能**  
一个键，用于指定可选性能监视的信息。 此项下的值指定驱动程序的性能 DLL 的名称，以及该 DLL 中某些导出函数的名称。 您可以使用驱动程序的 INF 文件中的 **AddReg** 条目向此子项添加值项。

 

