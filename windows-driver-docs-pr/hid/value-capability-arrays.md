---
title: 值功能数组
description: 值功能数组
keywords:
- 价值功能阵列 WDK HID
- 阵列 WDK HID
- 功能 WDK HID 集合
- 用法值阵列 WDK HID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d40428251bd2f4241d8e7d6768f8d450f4b6ad71
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820281"
---
# <a name="value-capability-arrays"></a>值功能数组





*值功能数组* 包含有关特定类型的 HID 报表的 [顶级集合](top-level-collections.md)支持的值使用情况的信息。 有关集合的值功能数组的信息包含在其 [**HIDP \_ cap**](/windows-hardware/drivers/ddi/hidpi/ns-hidpi-_hidp_caps) 结构中。

用户模式应用程序或内核模式驱动程序使用以下 [HIDClass 支持例程](/windows-hardware/drivers/ddi/index) 之一获取按钮功能信息：

-   [**HidP \_GetValueCaps**](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getvaluecaps) 返回值功能数组，它描述调用方指定的报表类型中包含的所有值。

-   [**HidP \_GetSpecificValueCaps**](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getspecificvaluecaps) 筛选由调用方指定的使用情况页、使用情况、链接集合和报表类型返回的值功能信息。

值功能数组包含 [**HIDP \_ 值 \_ cap**](/windows-hardware/drivers/ddi/hidpi/ns-hidpi-_hidp_value_caps) 结构，其中每个结构都描述了有关 [HID 使用情况](hid-usages.md) 或 [使用范围](hid-usages.md#usage-range)的下列信息：

-   使用情况或使用情况范围的[使用情况页](hid-usages.md#usage-page)

-   包含该值的报表的报表 ID

-   [使用 ID](hid-usages.md#usage-id)或使用范围

-   指示使用情况是否为[别名](hid-usages.md#aliased-usages)使用

-   有关包含用量或使用范围的 [链接集合](link-collections.md) 的信息

-   值的大小，以位为单位，报表计数 (是结构所描述的单个值的数目) 

-   每个值的属性，包括：是否具有 null 值、其单位和指数以及其逻辑和物理范围

-   与使用情况或使用情况范围关联的字符串描述符和指示符的相关信息

-   有关 HID 分析器分配使用情况或使用范围的 [数据索引](data-indices.md) 的信息

通常，以下条件适用于值功能数组描述的所有用法：

-   每个功能结构都表示一个使用情况、一个使用范围或与一个变量主项关联的 [使用情况值数组](#usage-value-array) 。 值不支持数组主要项。

-   可以使用别名使用。 使用范围不能有别名。 已化名为的值在值功能数组中链接在一起，其方式与在按钮功能数组中将它们链接在一起的别名按钮相同。 请参阅 [变量主项目中的按钮用法](button-capability-arrays.md#button-usages-in-a-variable-main-item)。

-   HID 分析器只使用为每个值分配使用情况所需的最少使用的用法。 分析器按在报表描述符中指定的顺序来分配使用情况。 不需要的报表描述符中的用法将被丢弃。 值功能数组不包含有关被丢弃的用法的任何信息。

-   HID 分析器为功能数组中所述的每个使用分配一个唯一的 [数据索引](data-indices.md) 。

有关如何将数据索引分配给值的说明，请参阅 [数据索引](data-indices.md)。

### <a name="usage-value-array"></a><a href="" id="usage-value-array"></a> 用法值数组

" *使用值" 数组* 是在主项目中指定的一组连续的值，所有这些值都分配了相同的使用量。 如果为报表计数大于1的主项仅指定了一个使用情况，则会发生这种情况。

下图显示了一个使用值数组的示例，其中每个数据项包含五个数据项。

![阐释包含5个数据项的使用值数组的图表，每个6位长](images/repcount.png)

在前面的示例中，此类使用量值数组的值功能结构将其 **IsRange** 成员设置为 **FALSE**，其 **NotRange** 成员设置为17，其 **ReportCount** 成员设置为5，其 **BitSize** 成员设置为6。

如果使用情况的报表计数为1，请使用 **HidP \_ GetUsageValue** 提取使用值。 如果使用情况的报表计数大于1，则 **HidP \_ GetUsageValue** 只返回用量值数组中的第一个数据项。 若要提取使用情况值数组中的所有数据项，请使用 [**HidP \_ GetUsageValueArray**](/windows-hardware/drivers/ddi/hidpi/nf-hidpi-hidp_getusagevaluearray)。

 

