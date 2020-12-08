---
title: '\_ \_ \_ \_ 来自 \_ 类型 \_ ID \_ 和 \_ U64 的 EXT TDOP SET PTR'
description: "\" \\_ \\_ \\_ \\_ \\_ \\_ 调试请求的类型 ID\" 和 \"U64\" 子操作的 ext TDOP SET PTR 将 \\_ \\_ \\_ \\_ \\_ \\_ \\_ 创建一个类型化的数据说明，该说明表示指向具有指定类型的指定内存位置的指针。"
keywords:
- EXT_TDOP_SET_PTR_FROM_TYPE_ID_AND_U64 Windows 调试
topic_type:
- apiref
api_name:
- EXT_TDOP_SET_PTR_FROM_TYPE_ID_AND_U64
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: cda061d0e0e172ce2c0722f0aeed342d4ccce3ae
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840211"
---
# <a name="ext_tdop_set_ptr_from_type_id_and_u64"></a>\_ \_ \_ \_ 来自 \_ 类型 \_ ID \_ 和 \_ U64 的 EXT TDOP SET PTR


" \_ \_ \_ \_ \_ \_ 调试请求的类型 ID" 和 "U64" 子操作的 ext TDOP SET PTR 将 \_ \_ 创建一个类型化的数据说明，该说明表示指向具有指定类型的指定内存位置的指针。 [**\_ \_ \_ \_ \_**](debug-request-ext-typed-data-ansi.md)[**Request**](request.md)

**Parameters**

<span id="Operation"></span><span id="operation"></span><span id="OPERATION"></span>**运作**  
将 \_ \_ \_ \_ \_ \_ \_ \_ 此子操作的类型 ID 和 U64 设置为 EXT TDOP set PTR。

<span id="Flags"></span><span id="flags"></span><span id="FLAGS"></span>**随意**  
指定用于描述类型化数据的值所在的目标内存的位标志。 有关这些标志的详细信息，请参阅 [**EXT \_ 类型化 \_ 数据**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data) 。

<span id="InData"></span><span id="indata"></span><span id="INDATA"></span>**InData**  
指定类型和内存位置。 可以手动创建并填充所需成员的 [**调试 \_ 类型化 \_ 数据**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_debug_typed_data) 结构的此实例。 使用以下成员：

<span id="ModBase"></span><span id="modbase"></span><span id="MODBASE"></span>**ModBase**  
指定包含类型的模块基址的目标虚拟内存中的位置。

<span id="Offset"></span><span id="offset"></span><span id="OFFSET"></span>**抵销**  
指定目标的数据内存中的位置。 **偏移量** 是虚拟内存地址，除非 **标志** 中存在指定该 **偏移量** 是物理内存地址的标志。

<span id="TypeId"></span><span id="typeid"></span><span id="TYPEID"></span>**TypeId**  
指定类型的类型 ID。

<span id="OutData"></span><span id="outdata"></span><span id="OUTDATA"></span>**OutData**  
接收表示指向内存位置和类型的指针的类型化数据说明。

<span id="Status"></span><span id="status"></span><span id="STATUS"></span>**状态值**  
接收此子操作返回的状态代码。 这与 [**请求**](request.md)返回的值相同。

<a name="remarks"></a>备注
-------

EXT \_ TDOP \_ SET \_ PTR \_ FROM \_ TYPE \_ ID \_ 和 \_ U64 是 [**ext \_ TDOP**](/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop) 枚举中的一个值。

此子操作的参数是 [**EXT \_ 类型化 \_ 数据**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data) 结构的成员。 \_ \_ 此子操作不使用上面的参数部分中未列出的 EXT 类型化数据的成员，并且应将其设置为零。 前面参数部分中的成员的说明指定了成员的用途。 有关更多详细信息，请参阅 **EXT \_ 类型化 \_ 数据** 。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**调试 \_ 请求 \_ EXT \_ 类型化 \_ 数据 \_ ANSI**](debug-request-ext-typed-data-ansi.md)

[**EXT \_ TDOP**](/windows-hardware/drivers/ddi/wdbgexts/ne-wdbgexts-_ext_tdop)

[**EXT \_ 类型化 \_ 数据**](/windows-hardware/drivers/ddi/wdbgexts/ns-wdbgexts-_ext_typed_data)

[**Request**](request.md)

 

