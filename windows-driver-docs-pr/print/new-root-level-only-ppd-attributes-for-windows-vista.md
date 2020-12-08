---
title: 适用于 Windows Vista 的仅限根级别的新 PPD 属性
description: 适用于 Windows Vista 的仅限根级别的新 PPD 属性
keywords:
- 仅限根级别的属性 WDK Unidrv
- 常规打印机属性 WDK Unidrv，仅限根级别
- PPD 属性 WDK Unidrv
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 09571744250e1bf1c2b0478cab5a430f918a435f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807791"
---
# <a name="new-root-level-only-ppd-attributes-for-windows-vista"></a>适用于 Windows Vista 的仅限根级别的新 PPD 属性


以下列表描述了从 Windows Vista 开始新增的 PPD 属性。 若要保持与 Windows Vista 以前版本的向后兼容性，应将这些属性包含在以下代码中。

```cpp
*Ifdef: WINNT_60 ... *Endif: WINNT_60 blocks
```

### <a name="msprintschemakeywordmap"></a>MSPrintSchemaKeywordMap

**MSPrintSchemaKeywordMap** 属性定义从 ppd 功能关键字到公共 print schema 功能关键字的映射，或从 ppd 功能的 ppd 选项关键字到打印架构功能的公共打印架构选项关键字的映射。

**MSPrintSchemaKeywordMap** 有两个可接受的格式：

<a href="" id="format-1"></a>格式1  
```cpp
*MSPrintSchemaKeywordMap: PrintSchema_feature_keyword *<PPD_feature_keyword>
```

<a href="" id="format-2"></a>格式2  
```cpp
*MSPrintSchemaKeywordMap: PrintSchema_feature_keyword PrintSchema_option_keyword *<PPD_feature_keyword> <PPD_option_keyword>
```

PPD 功能关键字前缀 (这 \[ \* \] 两种格式都需要星号) 。

对于格式1：

-   PPD 功能关键字必须引用已在上一 PPD 文件内容中定义的 PPD 功能。

-   \*对于同一 PPD 功能，不允许多个 **MSPrintSchemaKeywordMap** 定义。 如果找到多个定义，将只接受第一个定义，并且将忽略其他定义。

对于格式2：

-   \*通过使用 format 1)  ( 的 ppd 功能的 *_MSPrintSchemaKeywordMap_* 定义必须存在，然后才能 \* 显示 ppd 功能选项的任何 *_MSPrintSchemaKeywordMap_* 定义。

-   在 \* ppd 选项的 *_MSPrintSchemaKeywordMap_* 定义中，通过使用 format 1) ，将 ppd 功能关键字映射到打印架构功能关键字必须与在上一次 \* 使用 PPD (功能的 *_MSPrintSchemaKeywordMap_* 定义中定义的内容相同。

-   PPD 选项关键字必须引用已在上一 PPD 文件内容中定义的 PPD 功能选项。

-   \*不允许使用 ppd 功能的相同 ppd 选项的 *_MSPrintSchemaKeywordMap_* 的多个定义。 如果找到多个定义，将只接受第一个定义，并且将忽略其他定义。

如果 \* *_MSPrintSchemaKeywordMap_* 条目违反了前面的任何格式规则，则该条目将被忽略，并且你将收到包含详细信息的 ppdchecker 警告。

**重要说明**  
\*不支持将 MSPrintSchemaKeywordMap 用于以下标准的 PPD 功能：

\*逐 \* 工 \* InputSlot \* OutputBin \* PageSize \* 解析 \* 媒体。若要将某一功能映射到已在 PPD 文件中使用的 Print Schema 关键字，还必须知道相应的 PrintCapabilities 文档可能会多次列出该功能。 多次出现可能会造成混淆，因此，不应将功能映射到在 PPD 文件中使用的架构关键字。

 

**注意**  PPD 分析器会自动生成 InputBin 功能的 FORMSOURCE 选项，并将其映射到打印架构中的 "自动选择" 关键字。 如果 PPD 文件包含一个 InputBin 选项，该选项使用 **MSPrintSchemaKeywordMap** 特性将选项映射到 print schema 关键字，则打印架构中的功能将在设备命名空间中包含 FORMSOURCE 选项。 "自动选择" 将显示在 PrintCapabilities 文档中，并引用 PPD 文件的 " **MSPrintSchemaKeywordMap** " 属性中指定的选项。

 

下面的代码示例显示了部分 PPD 文件中的 **MSPrintSchemaKeywordMap** 属性的示例。

```cpp
*OpenUI *IHVStapling:PickOne
*DefaultIHVStapling:Disabled
*IHVStapling Enabled:"..."
*IHVStapling Disabled:"..."
*CloseUI: *IHVStapling

*MSPrintSchemaKeywordMap: Staple*IHVStapling
*MSPrintSchemaKeywordMap: StapleOn*IHVStaplingEnabled
*MSPrintSchemaKeywordMap: StapleOff*IHVStaplingDisabled
```

### <a name="msprintschemaprivatenamespaceuri"></a>MSPrintSchemaPrivateNamespaceURI

**MsPrintSchemaPrivateNamespaceURI** 特性定义核心驱动程序用于公开 PrintTicket 或 PrintCapabilities 中的私有 PPD 功能或选项的专用命名空间 URI。 此 URI 将应用于不具有显式映射的任何功能或选项 (通过使用 \* *_MSPrintSchemaKeywordMap_* 定义) 到公共打印架构。

**MSPrintSchemaPrivateNamespaceURI** 使用以下格式。

```cpp
*MSPPrintSchemaPrivateNamespaceURI: "<URI>"
```

&lt;URI &gt; 表示 PPD QuotedValue。 如 PPD 规范所定义的，QuotedValue 允许使用文本 ASCII 子字符串和十六进制子字符串。

单个打印机型号的 PPD 文件 (或文件) 应只有一个 \* **MSPrintSchemaPrivateNamespaceURI** 定义。 如果找到多个定义，将只接受第一个定义，而将忽略其他定义。

下面的代码示例显示了部分 PPD 文件中的 **MsPrintSchemaPrivateNamespaceURI** 属性的示例。

```cpp
*MSPrivateNamespaceURI:  "https://www.ihv.com/schema/2004"
```

### <a name="msisxpsdriver"></a>MSIsXPSDriver

**MSIsXPSDriver** 属性使用以下格式。

```cpp
*MSIsXPSDriver:  True | False
```

可以为 Microsoft Win32 GDI 驱动程序和 [新的 XPSDrv 驱动程序](xpsdrv-printer-drivers.md)使用 Windows Vista PScript5 驱动程序配置模块 ( # A0) 。 若要将 PScript5 驱动程序配置模块用于 XPSDrv 驱动程序，XPSDrv 驱动程序的 PPD 数据文件必须指定 **MSIsXPSDriver** 并将其值设置为 True。

下面的代码示例显示了部分 PPD 文件中此特性的示例：

```cpp
*MSIsXPSDriver: True
```

若要将 PScript5 驱动程序配置模块用于 Win32 GDI 驱动程序，无需指定此 PPD 特性。

### <a name="msprintprocduplexoptions"></a>MSPrintProcDuplexOptions

**MSPrintProcDuplexOptions** 属性使用以下格式。

```cpp
*MSPrintProcDuplexOptions:  "int"
```

此属性可以具有以下值之一：

1：反向双工页

2：如果可能，禁止生成额外的空白页

3：上述两个

0：以上均不是

下面的代码示例显示了部分 PPD 文件中 **MSPrintProcDuplexOptions** 的示例。

```cpp
*MSPrintProcDuplexOptions:  "2" 
```

此属性控制打印处理器中的各种双工选项。

如果 **MSPrintProcDuplexOptions** 为1，则它控制打印处理器是否应反转双工上的页面。

假设您必须打印一个包含 n-up = 1 的四页文档，并且您想要使用反转打印和双工打印。 由于需要进行反向打印，因此需要在第一页之前打印最后一页。 由于需要双面打印，因此需要在一张纸上打印两页。 打印处理器可以使用以下两种格式中的一种来播放页 (其中，每对数字表示将在单张纸的两面上打印的两页) ：

-   格式1： (4，3) ， (2，1) 

-   格式2： (3，4) ， (1，2) 

在 Windows Vista 之前，打印处理器会打印格式为 2 \[ (3，4) ， (1，2) 的页面 \] 。 但在 Windows Vista 和更高版本中，默认格式为 format 1 \[ (4，3) ， (2，1) \] 。 发生此更改的原因是许多打印机的输出格式不正确，格式为 2;也就是说，打印的页面未按正确顺序排列。

如果你的打印机在格式为1的情况下正常工作，则不需要为 Windows Vista 和更高版本更改任何内容。 但是，如果您的打印机的格式不正确，并且您希望恢复为格式2，请添加值为1的 **MSPrintProcDuplexOptions** 属性。

```cpp
*MSPrintProcDuplexOptions: "1"
```

对于 Windows Vista 之前的 PScript 驱动程序，如果你具有 Windows Vista 以前的打印处理器，则默认情况下，"格式 2" 为默认值，并且你无法更改该行为;否则，如果你有 Windows Vista 打印处理器，则默认情况下将使用格式1，并且你无法更改该行为。

对于 Windows Vista PScript 驱动程序。 如果使用的是 Windows Vista 以前的打印处理器，则默认情况下将忽略格式2，并忽略 PPD 属性;否则，如果你有 Windows Vista 打印处理器，则默认情况下使用格式1，但你可以使用 **MSPrintProcDuplexOptions** 属性更改格式。

如果 **MSPrintProcDuplexOptions** 为2，则打印处理器将禁止在某些双工方案中生成空白页。

例如，如果作业为单页作业，并且双工处于开启状态 (假设 n 向上 = 1) ，则只需打印纸张的一侧。 目前，打印机将打印一侧，然后在反面生成空的空白页。  (因为打印作业是以双工 = on 启动的，所以打印机在弹出工作表之前需要两个页面。 如果第二个页面未打印，则某些打印机会继续等待。 ) 当前解决方案的缺点：

-   生成的页面会导致会计软件中的页计数不准确，以及打印机中的页计数器。

-   如果页面上的 Hewlett Packard DeskJet) 打印机中的页面的 (一半，则用户可能会尝试将其拉出，同时打印机会尝试将其取回。 这种情况可能导致硬件问题。

可以通过 \* 在 PPD 文件中指定 *_MSPrintProcDuplexOptions_*： "2" 来避免上述问题。

请注意，即使设置了此属性，仅在以下有限情况下才会执行空白页面优化：

1.  对于反向打印，仅当整个作业可以放在一侧纸上时才执行空白页面优化 (例如，aone = 1 的页面作业，以及包含 n 个) 的四页作业。 如果作业需要多个工作表，则不会执行优化 (因为打印机页将按不准确的顺序打印) 。 例如，对于三页作业，可以按订单3、2、1、 &lt; 空白 &gt; 而不是4，3，2，将页面打印为 &lt; 空白 &gt; 。

2.  如果打印处理器必须模拟副本，则不会 performedd 空白页优化。 如果所需的副本数大于打印处理器可以制作的副本数，打印处理器会模拟副本。

    以下情况是发生模拟的一个示例，并 (如有必要) 生成空白页：

    -   不能制作副本的打印机的两个副本

    以下情况 examles 不发生模拟时的情况，您可以取消额外的页面生成：

    -   不能制作副本的打印机的单个复制作业
    -   5-复制作业，适用于可以制作超过个副本的打印机

对于 Windows Vista 之前的 PScript 驱动程序，如果有 Windows Vista 以前的打印处理器，打印机将打印一个额外的空白页面（如果有必要），并且无法更改该行为;否则，如果有 Windows Vista 打印处理器，打印机将打印额外的空白页面（如果有必要），并且无法更改行为。

对于 Windows Vista PScript 驱动程序。 如果使用的是 Windows Vista 以前的打印处理器，则打印机将打印额外的空白页面（如果有必要），并且将忽略 PPD 属性;否则，如果你有一个 Windows Vista 打印处理器，并且有适当的 PPD 属性和合适的条件 (也就是说，先前介绍的用于防止空白页面打印) 的情况下，打印机将不会打印空白页面。

### <a name="msbidiqueryfile"></a>MSBidiQueryFile

**MSBiDiQueryFile** 属性使用以下格式。

```cpp
*MSBidiQueryFile: "filename"
```

使用 **MSBiDiQueryFile** 指定 GPD 或 GDL 文件名，其中包含打印机驱动程序的自动配置 BidiQuery 和 BidiResponse 数据。 GPD 或 GDL 文件名不应指定任何路径。

下面的代码示例显示了部分 PPD 文件中 **MSBiDiQueryFile** 的示例。

```cpp
*MSBidiQueryFile: "ACnfgPS.GDL"
```

### <a name="msxpsmaxcopies"></a>MSXPSMaxCopies

**MSXPSMaxCopies** 属性使用以下格式。

```cpp
*MSXPSMaxCopies: "int"
```

使用 **MSXPSMaxCopies** 指定 XPSDrv 打印机驱动程序可以支持的最大副本数。

下面的代码示例显示了部分 PPD 文件中 **MSXPSMaxCopies** 的示例。

```cpp
*MSXPSMaxCopies: "99"
```

 

 




