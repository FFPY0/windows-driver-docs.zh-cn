---
title: 替换驱动程序提供的属性表页
description: 替换驱动程序提供的属性表页
keywords:
- 用户界面插件 WDK 打印，属性表页面
- UI 插件 WDK 打印，属性表单页面
- 属性表页 WDK 打印
- 替换属性表页
- IPrintCoreUI2
- 文档-粘滞属性 WDK 打印
- 打印机-粘滞属性 WDK 打印
- 设备-粘滞属性 WDK 打印
- 粘滞属性 WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67ae267ab79c403f0d6cd7f498ae1a799239bf4e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807039"
---
# <a name="replacing-driver-supplied-property-sheet-pages"></a>替换驱动程序提供的属性表页





[IPRINTCOREUI2 COM 接口](iprintcoreui2-com-interface.md)提供了四种方法，在 windows XP 和更高版本的 windows 操作系统上运行的 Pscript5 UI 插件在打算完全替换核心驱动程序的标准 UI 页时必须使用。  (术语 "核心驱动程序" 指的是 Unidrv 或 Pscript5 打印机驱动程序。 ) 这些方法如下所示：

[**IPrintCoreUI2::EnumConstrainedOptions**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-enumconstrainedoptions)

[**IPrintCoreUI2::GetOptions**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-getoptions)

[**IPrintCoreUI2：： SetOptions**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-setoptions)

[**IPrintCoreUI2::WhyConstrained**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-whyconstrained)

仅在 UI 插件的 [**IPrintOemUI：:D ocumentpropertysheets**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-documentpropertysheets) 和 [**IPrintOemUI：:D evicepropertysheets**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-devicepropertysheets) 方法及其属性表回调例程的执行过程中，才支持这些方法。 UI 插件支持这些方法以显示其自己的用户界面。 如果不支持，这些方法将返回 E \_ NOTIMPL。

核心驱动程序在两个环境中显示其自己的属性表 UI--对于 [**DrvDocumentPropertySheets**](/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdocumentpropertysheets)，为 [**DrvDevicePropertySheets**](/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvdevicepropertysheets)。 第一种方法显示仅适用于) 文档 (文档的属性，第二种方法显示应用于设备的属性， (设备或打印机粘滞属性) 。

核心驱动程序会记住它处理 (的属性表类型，因此，模式--文档粘滞或打印机粘滞) 。 核心驱动程序将该状态信息保存在结构 () 为 UI 实例创建的 [**OEMUIOBJ**](/windows-hardware/drivers/ddi/printoem/ns-printoem-_oemuiobj) 结构。 当核心驱动程序调用插件的接口方法时，它会传递一个指向 OEMUIOBJ 结构的指针，以便当插件从 [**IPrintCoreUI2：： EnumConstrainedOptions**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-enumconstrainedoptions)、 [**IPrintCoreUI2：： GetOptions**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-getoptions)、 [**IPrintCoreUI2：： SetOptions**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-setoptions)或 [**IPrintCoreUI2：： WhyConstrained**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-whyconstrained)返回到核心驱动程序时，这些方法会将指针传递回核心驱动程序，然后它便能够确定模式。

对于 **IPrintCoreUI2：： EnumConstrainedOptions**、 **IPrintCoreUI2：： SetOptions** 和 **IPrintCoreUI2：： WhyConstrained**，在执行 **IPrintOemUI：:D ocumentpropertysheets** 或其属性表回调例程期间仅支持文档粘滞功能，并且在执行 **IPrintOemUI：:D evicepropertysheets** 或其属性表回调例程期间仅支持打印机粘滞功能。 对于 **IPrintCoreUI2：： SetOptions**，应忽略与当前粘滞模式不匹配的任何功能。 当对其粘性与当前粘滞模式不匹配的功能调用 **IPrintCoreUI2：： EnumConstrainedOptions** 或 **IPrintCoreUI2：： WhyConstrained** 时，该方法应返回 E \_ INVALIDARG。

对于 [**IPrintCoreUI2：： GetOptions**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintcoreui2-getoptions)，文档粘滞模式支持文档粘滞和打印机粘滞功能 (即，当 [**IPrintOemUI：:D ocumentpropertysheets**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-documentpropertysheets) 或其属性表回调例程正在) 运行时，仅当 [**IPrintOemUI：:D evicepropertysheets**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-devicepropertysheets) 或其属性表回调例程正在运行时，才支持打印机粘滞模式 (。

 

