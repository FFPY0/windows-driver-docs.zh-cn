---
title: 特定于 PPD 的接口
description: 特定于 PPD 的接口
keywords:
- PostScript 打印机驱动程序 WDK 打印，特定于 PPD 的接口
- Pscript WDK 打印，特定于 PPD 的接口
- IPrintCoreUI2
- PPD 文件 WDK Pscript
- PPD 特定于 PPD 的接口 WDK Pscript
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 285a7bcae4e57ac6f4ad93a01d75b038f010fb0e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807527"
---
# <a name="ppd-specific-interface"></a>特定于 PPD 的接口





[IPRINTCOREUI2 COM 接口](iprintcoreui2-com-interface.md)支持九种用户界面插件可调用以访问 *PPD* 文件中的信息的方法。 其中六种方法在 [IPRINTCOREPS2 COM 接口](iprintcoreps2-com-interface.md)中受支持。 本部分介绍这些方法的 PPD 特定行为。

### <a name="iprintcoreui2-interface-ppd-methods"></a>IPrintCoreUI2 接口 PPD 方法

[**IPrintCoreUI2::EnumConstrainedOptions**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-enumconstrainedoptions)

[**IPrintCoreUI2::EnumFeatures**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-enumfeatures)

[**IPrintCoreUI2::EnumOptions**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-enumoptions)

[**IPrintCoreUI2::GetOptions**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-getoptions)

[**IPrintCoreUI2::GetFeatureAttribute**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-getfeatureattribute)

[**IPrintCoreUI2::GetGlobalAttribute**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-getglobalattribute)

[**IPrintCoreUI2::GetOptionAttribute**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-getoptionattribute)

[**IPrintCoreUI2：： SetOptions**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-setoptions)

[**IPrintCoreUI2::WhyConstrained**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-whyconstrained)

### <a name="iprintcoreps2-interface-ppd-methods"></a>IPrintCorePS2 接口 PPD 方法

[**IPrintCorePS2::EnumFeatures**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreps2-enumfeatures)

[**IPrintCorePS2::EnumOptions**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreps2-enumoptions)

[**IPrintCorePS2::GetOptions**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreps2-getoptions)

[**IPrintCorePS2::GetFeatureAttribute**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreps2-getfeatureattribute)

[**IPrintCorePS2::GetGlobalAttribute**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreps2-getglobalattribute)

[**IPrintCorePS2::GetOptionAttribute**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreps2-getoptionattribute)

在本节中，对作为这两个接口的成员的任何方法的引用都适用于这两种方法。 例如，对 **GetOptions** 的引用适用于 **IPrintCoreUI2：： GetOptions** 和 **IPrintCorePS2：： GetOptions**。

### <a name="ppd-feature-availability"></a>PPD 功能可用性

请注意，在本部分中，"PPD 功能当前不可用" 一词表示打印机不支持该功能，或者该功能的 "非空"/"False" 选项受当前可安装选项设置的约束。

例如，"双工功能当前不可用" 表示 PPD 未指定 \* *_双工_* 功能关键字，或 \* *_双工_* 功能关键字的非 None 选项当前受双工单元未安装这一事实的限制。

 

