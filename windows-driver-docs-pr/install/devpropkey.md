---
title: DEVPROPKEY 结构
description: 在 Windows Vista 和更高版本的 Windows 中，DEVPROPKEY 结构表示统一设备属性模型中设备属性的设备属性键。
keywords:
- DEVPROPKEY 结构设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPROPKEY
api_location:
- devpropdef.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 887296b6209141279b1811e68724a67bda6fb77b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803557"
---
# <a name="devpropkey-structure"></a>DEVPROPKEY 结构


在 Windows Vista 和更高版本的 Windows 中，DEVPROPKEY 结构表示 [统一设备属性模型](./unified-device-property-model--windows-vista-and-later-.md)中设备属性的设备属性键。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
struct DEVPROPKEY {
  DEVPROPGUID fmtid;
  DEVPROPID   pid;
};
```

<a name="members"></a>成员
-------

**fmtid**  
指定属性类别的 DEVPROPGUID 类型的值。

DEVPROPGUID 数据类型定义为：

```cpp
typedef GUID  DEVPROPGUID, *PDEVPROPGUID;
```

pid  
一个 DEVPROPID 类型的值，该值唯一标识属性类别中的属性。 由于内部系统原因，属性标识符必须大于或等于2。

DEVPROPID 数据类型定义为：

```cpp
typedef ULONG DEVPROPID, *PDEVPROPID;
```

<a name="remarks"></a>备注
-------

DEVPROPKEY 结构是 [统一设备属性模型](./unified-device-property-model--windows-vista-and-later-.md)的一部分。

系统提供的设备属性键的基本集是在 *Devpkey* 中定义的。

[**DEFINE \_ DEVPROPKEY**](./define-devpropkey.md)宏创建表示设备属性键的 DEVPROPKEY 结构的实例。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>标头</p></td>
<td align="left">Devpropdef (包含 Devpropdef) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**定义 \_ DEVPROPKEY**](./define-devpropkey.md)

 

