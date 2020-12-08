---
title: INF DriverVer 指令
description: DriverVer 指令指定此 INF 安装的驱动程序的版本信息。
keywords:
- INF DriverVer 指令设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF DriverVer Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ae5505ac7e210ff3831925c6cc64c45266c41775
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813105"
---
# <a name="inf-driverver-directive"></a>INF DriverVer 指令


**DriverVer** 指令指定此 INF 安装的驱动程序的版本信息。

```inf
[Version] |
[DDInstall]
 
DriverVer=mm/dd/yyyy,w.x.y.z 
```

## <a name="entries"></a>项


<a href="" id="mm-dd-yyyy"></a>*mm/dd/yyyy*  
此值指定 "[驱动程序包](driver-packages.md)" 的日期，其中包含驱动程序文件和 INF。 此日期必须是驱动程序包中任何文件的最新日期。

必须按月/日/年顺序指定日期。 月份和日期必须包含两位数，年份必须包含四位数字。 连字符 ( ) 可用作日期字段分隔符，而不能用作斜杠 (/) 。

<a href="" id="w-x-y-z"></a>*w.x.y.z. z*  
此值指定版本号。

每个 *w*、 *x*、 *y* 和 *z* 都必须是大于或等于零且小于65535的整数。

对于 Windows XP SP1、Windows Server 2003 和更高版本的 Windows，安装程序也将此值与驱动程序的排名和日期结合 *使用* ，以选择设备的驱动程序。 有关详细信息，请参阅 [Windows 如何选择驱动程序](./how-windows-selects-a-driver-for-a-device.md)。

以下点适用于 Windows 2000 和 Windows XP 的此值：

-   应将此值视为 (的输入驱动程序所必需的值，例如鼠标或键盘驱动程序) 。 如果不包含版本值，则可能无法以编程方式更新输入驱动程序。 通常，应在所有 [驱动程序包](driver-packages.md) 中指定版本信息，因为操作系统使用版本信息作为确定最新驱动程序的条件。

<a name="remarks"></a>备注
-------

从 Windows 2000 开始，INF 文件必须在其 [**INF 版本部分**](inf-version-section.md)中有一个 **DriverVer** 指令，以便为整个 INF 提供版本信息。 单个 [**INF *DDInstall* 节**](inf-ddinstall-section.md) 还可包含 **DriverVer** 指令，以提供各个驱动程序的版本信息。 *DDInstall* 部分中的 **DriverVer** 指令更为具体，并优先于 **版本** 部分中的全局 **DriverVer** 指令。

当操作系统搜索驱动程序时，它会选择一个在具有较早日期的驱动程序上具有最新 **DriverVer** 日期的驱动程序。 如果 INF 没有 **DriverVer** 指令或包含无效的日期规范，则操作系统将应用默认日期00/00/0000。 仅适用于 Windows 2000，未签名的驱动程序的日期为00/00/0000。

<a name="examples"></a>示例
--------

```inf
[Version]
...
DriverVer=09/28/1999,5.00.2136.1
```

## <a name="see-also"></a>另请参阅


[**_DDInstall_* _](inf-ddinstall-section.md)

[_ *版本**](inf-version-section.md)

 

