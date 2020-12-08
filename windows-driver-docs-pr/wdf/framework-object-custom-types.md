---
title: 框架对象自定义类型
description: 框架对象自定义类型
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dbed9508c13ba967cb507d7ff5aa74afd8a13619
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814785"
---
# <a name="framework-object-custom-types"></a>框架对象自定义类型


从 KMDF 版本1.11 开始，框架支持自定义类型名称。 自定义类型名称是一个字符串，驱动程序可以将该字符串与 WDFOBJECT 实例相关联。 驱动程序定义自己的自定义类型名称。 驱动程序在调用对象的创建方法之后，为对象指定自定义类型名称。

使用以下宏操作自定义类型名称：

-   若要定义自定义类型名称，请从声明全局数据的驱动程序区域（如标头文件）中调用 [**WDF \_ 声明 \_ 自定义 \_ 类型**](./wdf-declare-custom-type.md) 。
-   调用 [**WdfObjectAddCustomType**](./wdfobjectaddcustomtype.md) 或 [**WdfObjectAddCustomTypeWithData**](./wdfobjectaddcustomtypewithdata.md) 将自定义类型与框架对象相关联。
-   调用 [**WdfObjectIsCustomType**](./wdfobjectiscustomtype.md) 以确定指定的对象是否为指定的自定义类型。
-   在调用 [**WdfObjectAddCustomTypeWithData**](./wdfobjectaddcustomtypewithdata.md)之后，驱动程序稍后可以调用 [**WdfObjectGetCustomTypeData**](./wdfobjectgetcustomtypedata.md) 来检索数据。

驱动程序可以将多个自定义类型与一个框架对象相关联。 驱动程序还可以将多个框架对象与一个自定义类型关联。

在 KMDF 调试器扩展的输出中，自定义类型名称与其他 WDF 对象信息一起显示。

```cpp
WDF_Object_Name, [custom_Type1_Name, custom_Type2_Name]
```

 

