---
title: 颜色属性
description: 颜色属性
keywords:
- 颜色属性 WDK Unidrv
- 常规打印机属性 WDK Unidrv，color
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 91aa71108c321d697dbbd67e1e13a72faecf5b5d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797707"
---
# <a name="color-attributes"></a>颜色属性





颜色属性是 [常规打印属性](general-printing-attributes.md) ，用于指定控制彩色打印的特征。

下表列出了颜色属性。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>属性名称</th>
<th>特性参数</th>
<th>注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong><em>ChangeColorModeOnDoc?</strong></p></td>
<td><p><strong>TRUE</strong> 或 <strong>FALSE</strong>。 指示是否可以在文档的页面之间更改打印机的颜色模式，而不会有副作用。</p></td>
<td><p>可选。 如果未指定，则默认值为 <strong>TRUE</strong>。 Unidrv 使用此值来优化打印速度。 有关其他信息，请参阅此表后面的注释。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>CyanInMagentaDye</strong></p></td>
<td><p>数值，介于0到1000之间，表示洋红色彩色的青色污染百分比。 值是100的污染百分比。 例如，8.4% 污染指定为840，10% 表示为1000。</p></td>
<td><p>可选。 如果未指定，则使用 Unidrv 提供的默认值。</p></td>
</tr>
<tr class="odd">
<td><p><strong><em>CyanInYellowDye</strong></p></td>
<td><p>数值，介于0到1000之间，表示以黄色彩色表示的青色污染的百分比。 值是100的污染百分比。 例如，8.4% 污染指定为840，10% 表示为1000。</p></td>
<td><p>可选。 如果未指定，则使用 Unidrv 提供的默认值。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>EnableGDIColorMapping</strong></p></td>
<td><p><strong>TRUE</strong> 或 <strong>FALSE</strong>。 指示 GDI 是否应执行从显示到打印机颜色空间的 gamut 映射。</p></td>
<td><p>可选。 如果未指定，则默认值为 <strong>FALSE</strong>。 如果 <strong>为 TRUE</strong>，则 Unidrv 设置 <a href="/windows/win32/api/winddi/ns-winddi-gdiinfo" data-raw-source="[&lt;strong&gt;GDIINFO&lt;/strong&gt;](/windows/win32/api/winddi/ns-winddi-gdiinfo)"><strong>GDIINFO</strong></a> 结构中的 HT_FLAG_DO_DEVCLR_XFORM 标志。</p></td>
</tr>
<tr class="odd">
<td><p><strong><em>MagentaInCyanDye</strong></p></td>
<td><p>数值，介于0到1000之间，表示青色彩色的洋红色污染百分比。 值是100的污染百分比。 例如，8.4% 污染指定为840，10% 表示为1000。</p></td>
<td><p>可选。 如果未指定，则使用 Unidrv 提供的默认值。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>MagentaInYellowDye</strong></p></td>
<td><p>数值，介于0到1000之间，表示黄色彩色的洋红色污染百分比。 值是100的污染百分比。 例如，8.4% 污染指定为840，10% 表示为1000。</p></td>
<td><p>可选。 如果未指定，则使用 Unidrv 提供的默认值。</p></td>
</tr>
<tr class="odd">
<td><p><strong><em>YellowInCyanDye</strong></p></td>
<td><p>数值，介于0到1000之间，表示青色彩色的黄色污染百分比。 值是100的污染百分比。 例如，8.4% 污染指定为840，10% 表示为1000。</p></td>
<td><p>可选。 如果未指定，则使用 Unidrv 提供的默认值。</p></td>
</tr>
<tr class="even">
<td><p><strong></em>YellowInMagentaDye</strong></p></td>
<td><p>数值，介于0到1000之间，表示洋红色彩色的黄色污染百分比。 值是100的污染百分比。 例如，8.4% 污染指定为840，10% 表示为1000。</p></td>
<td><p>可选。 如果未指定，则使用 Unidrv 提供的默认值。</p></td>
</tr>
</tbody>
</table>

 

**注意**  当 **\* ChangeColorModeOnDoc？** color 属性设置为 **TRUE** 时，会启用颜色优化。 如果此属性设置为 **FALSE**，则不执行任何优化。 启用颜色优化后，假脱机文件中的颜色将导致以彩色播放假脱机文件;假脱机文件中缺少颜色会导致后台处理文件以单色播放。
如果要创建 Unidrv 呈现插件来生成颜色水印，请注意，当颜色水印打印在黑白文档上时，将会导致彩色水印打印为黑白。 若要确保颜色水印正确地打印彩色和黑白文档，请禁用颜色优化。

通过设置 " **\* ChangeColorModeOnDoc？** color" 属性的 " **dwColorOptimization** " 成员，还可以控制由 "[**属性 \_ 信息 \_ 2**](/windows-hardware/drivers/ddi/winddiui/ns-winddiui-_attribute_info_2) " 或 "[**属性 \_ 信息 \_ 3**](/windows-hardware/drivers/ddi/winddiui/ns-winddiui-_attribute_info_3) " 结构控制的颜色优化。 还可以通过使用 [**GdiEndPageEMF**](/windows-hardware/drivers/ddi/winppi/nf-winppi-gdiendpageemf) 函数来控制颜色优化。

 

有关此页上列出的颜色属性的示例，请参阅 [示例 GPD 文件](sample-gpd-files.md)。

