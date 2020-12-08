---
title: WDF_OBJECT_ATTRIBUTES_SET_CONTEXT_TYPE 宏
description: WDF_OBJECT_ATTRIBUTES_SET_CONTEXT_TYPE 宏会将对象的驱动程序定义的上下文信息插入对象的 WDF_OBJECT_ATTRIBUTES 结构。
keywords:
- WDF_OBJECT_ATTRIBUTES_SET_CONTEXT_TYPE 宏
ms.date: 08/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: f0af9f1c4fba83cda4686f1d9747482f4483f939
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96809791"
---
# <a name="wdf_object_attributes_set_context_type-macro"></a>WDF_OBJECT_ATTRIBUTES_SET_CONTEXT_TYPE 宏


\[适用于 KMDF 和 UMDF\]

WDF_OBJECT_ATTRIBUTES_SET_CONTEXT_TYPE 宏会将对象的驱动程序定义的上下文信息插入对象的 [**WDF_OBJECT_ATTRIBUTES**](/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes) 结构。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
void WDF_OBJECT_ATTRIBUTES_SET_CONTEXT_TYPE(
    _attributes,
    _contexttype
);
```

<a name="parameters"></a>参数
----------

*_attributes*   
指向对象的 [**WDF_OBJECT_ATTRIBUTES**](/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes) 结构的指针。

*_contexttype*   
驱动程序定义的结构的结构类型名称，该结构描述对象的上下文空间的内容。

<a name="return-value"></a>返回值
------------

此宏不返回值。

<a name="remarks"></a>备注
-------

调用 [**WDF_OBJECT_ATTRIBUTES_INIT**](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdf_object_attributes_init)后，应使用 WDF_OBJECT_ATTRIBUTES_SET_CONTEXT_TYPE 宏。

有关使用 WDF_OBJECT_ATTRIBUTES_SET_CONTEXT_TYPE 宏的详细信息，请参阅 [框架对象上下文空间](./framework-object-context-space.md)。

有关使用此宏的代码示例，请参阅 [**WDF_DECLARE_CONTEXT_TYPE**](wdf-declare-context-type.md)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>目标平台</p></td>
<td><a href="https://go.microsoft.com/fwlink/p/?linkid=531356" data-raw-source="[Universal](https://go.microsoft.com/fwlink/p/?linkid=531356)">通用</a></td>
</tr>
<tr class="even">
<td><p>最低 KMDF 版本</p></td>
<td><p>1.0</p></td>
</tr>
<tr class="odd">
<td><p>最小 UMDF 版本</p></td>
<td><p>2.0</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Wdfobject (包含 Wdf .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**WDF_DECLARE_CONTEXT_TYPE**](wdf-declare-context-type.md)

[**WDF_OBJECT_ATTRIBUTES**](/windows-hardware/drivers/ddi/wdfobject/ns-wdfobject-_wdf_object_attributes)

[**WDF_OBJECT_ATTRIBUTES_INIT**](/windows-hardware/drivers/ddi/wdfobject/nf-wdfobject-wdf_object_attributes_init)

[**WDF_OBJECT_ATTRIBUTES_INIT_CONTEXT_TYPE**](wdf-object-attributes-init-context-type.md)

 

