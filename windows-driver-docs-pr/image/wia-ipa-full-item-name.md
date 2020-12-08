---
title: WIA \_ IPA \_ 完整 \_ 项 \_ 名称
description: WIA \_ IPA \_ full \_ item \_ name 属性包含项名称 (项名称的完整项名称) 的路径信息。
keywords:
- WIA_IPA_FULL_ITEM_NAME 图像设备
topic_type:
- apiref
api_name:
- WIA_IPA_FULL_ITEM_NAME
api_location:
- Wiadef.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c16385ab989c1c019a7e7343f70a845b8db739e6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817301"
---
# <a name="wia_ipa_full_item_name"></a>WIA \_ IPA \_ 完整 \_ 项 \_ 名称


WIA \_ IPA \_ full \_ item \_ name 属性包含项名称 (项名称的完整项名称) 的路径信息。

## <span id="ddk_wia_ipa_full_item_name_si"></span><span id="DDK_WIA_IPA_FULL_ITEM_NAME_SI"></span>


属性类型： VT \_ BSTR

有效值： WIA " \_ \_ 无"

访问权限：只读

<a name="remarks"></a>备注
-------

*完整的项名称* 与 [**wiasCreateDrvItem**](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatedrvitem)服务实用工具函数的 *bstrFullItemName* 参数相同。 应用程序读取 "WIA \_ IPA \_ FULL \_ ITEM \_ NAME" 属性，以确定它当前使用的项以及该项在 WIA 项树中的位置。 每个项都应具有唯一的名称。 应用程序通常使用完整项名称在 WIA 项树中搜索项。 WIA 服务创建并维护 WIA \_ IPA \_ 的完整 \_ 项 \_ 名称。

应用程序读取 WIA \_ IPA 的 \_ 完整 \_ 项 \_ 名称，以确定要接收的图像的格式。 应用程序写入此属性以设置格式。 WIA \_ IPA \_ 完整 \_ 项 \_ 名称取决于 [**WIA \_ IPA \_ TYMED**](wia-ipa-tymed.md) 属性。 WIA 微型驱动程序创建并维护 WIA \_ IPA \_ 完整 \_ 项 \_ 名称。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Wiadef (包含 Wiadef) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**IWiaMiniDrvTransferCallback：： GetNextStream**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrvtransfercallback-getnextstream)

[**WIA \_ IPA \_ TYMED**](wia-ipa-tymed.md)

[**wiasCreateDrvItem**](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatedrvitem)

 

