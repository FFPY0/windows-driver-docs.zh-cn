---
title: GDI 用户对象
description: GDI 用户对象
keywords:
- GDI WDK Windows 2000 显示，用户对象
- 图形驱动程序 WDK Windows 2000 显示，用户对象
- 绘制 WDK GDI，用户对象
- 用户对象 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8463b2a6688db169eae05b72e5ca18d612d64782
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822513"
---
# <a name="gdi-user-objects"></a>GDI 用户对象


## <span id="ddk_gdi_user_objects_gg"></span><span id="DDK_GDI_USER_OBJECTS_GG"></span>


GDI 维护重要的内部数据结构，但通过将它们作为 *用户对象* 向下传递来为驱动程序提供对这些结构的公共字段的访问权限。 用户对象是中间的数据结构，它们提供 GDI 数据结构与需要访问这些结构中信息的驱动程序之间的接口。 驱动程序可以将用户对象的指针传递回 GDI，以查询信息或要求提供各种服务。 具有公共字段的用户对象具有以下优点：

-   它们消除了与直接访问内部 GDI 数据结构相关的问题。

-   它们为驱动程序提供保存 GDI 数据的位置。 例如，PATHOBJ 结构可以保存枚举复杂对象（如路径）所需的所有额外数据。

可用的用户对象如下：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">对象</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/ns-winddi-brushobj" data-raw-source="[&lt;strong&gt;BRUSHOBJ&lt;/strong&gt;](/windows/win32/api/winddi/ns-winddi-_brushobj)"><strong>BRUSHOBJ</strong></a></p></td>
<td align="left"><p>为输出线条、文本或填充的图形函数定义画笔对象。 驱动程序可以调用 <a href="/windows-hardware/drivers/#wdkgloss-brushobj" data-raw-source="&lt;em&gt;BRUSHOBJ&lt;/em&gt;"><em>BRUSHOBJ</em></a> 服务来实现画笔，或查找以前由 GDI 缓存的实现。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/ns-winddi-clipobj" data-raw-source="[&lt;strong&gt;CLIPOBJ&lt;/strong&gt;](/windows/win32/api/winddi/ns-winddi-_clipobj)"><strong>CLIPOBJ</strong></a></p></td>
<td align="left"><p>为驱动程序提供对 <a href="/windows-hardware/drivers/#wdkgloss-clip-region" data-raw-source="&lt;em&gt;clip region&lt;/em&gt;"><em>剪辑区域</em></a> 的访问权限，以便进行绘制或填充。 可以将此区域枚举为一系列矩形。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/ns-winddi-floatobj" data-raw-source="[&lt;strong&gt;FLOATOBJ&lt;/strong&gt;](/windows/win32/api/winddi/ns-winddi-_floatobj)"><strong>FLOATOBJ</strong></a></p></td>
<td align="left"><p>允许图形驱动程序模拟浮点运算。 对于所有其他内核模式驱动程序，将禁用浮点运算。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/ns-winddi-fontobj" data-raw-source="[&lt;strong&gt;FONTOBJ&lt;/strong&gt;](/windows/win32/api/winddi/ns-winddi-_fontobj)"><strong>FONTOBJ</strong></a></p></td>
<td align="left"><p>为驱动程序提供有关特定实例的信息的访问 (或实现某个字体) 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/ns-winddi-palobj" data-raw-source="[&lt;strong&gt;PALOBJ&lt;/strong&gt;](/windows/win32/api/winddi/ns-winddi-_palobj)"><strong>PALOBJ</strong></a></p></td>
<td align="left"><p>包含 RGB 调色板颜色的结构;可通过 <a href="/windows/win32/api/winddi/nf-winddi-palobj_cgetcolors" data-raw-source="&lt;strong&gt;PALOBJ_cGetColors&lt;/strong&gt;"><em>PALOBJ</em></a> 结构访问不包含公共成员。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/ns-winddi-pathobj" data-raw-source="[&lt;strong&gt;PATHOBJ&lt;/strong&gt;](/windows/win32/api/winddi/ns-winddi-_pathobj)"><strong>PATHOBJ</strong></a></p></td>
<td align="left"><p>定义一个路径，该路径指定)  (线条或贝塞尔曲线绘制的内容。 <a href="/windows-hardware/drivers/#wdkgloss-pathobj" data-raw-source="&lt;em&gt;PATHOBJ&lt;/em&gt;"><em>PATHOBJ</em></a>结构将传递给驱动程序，以描述要描边或填充的一组直线和贝塞尔曲线。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/ns-winddi-strobj" data-raw-source="[&lt;strong&gt;STROBJ&lt;/strong&gt;](/windows/win32/api/winddi/ns-winddi-_strobj)"><strong>STROBJ</strong></a></p></td>
<td align="left"><p>为驱动程序枚举一个标志符号句柄和位置的列表，这些位置描述文本字符串的绘制方式。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/ns-winddi-surfobj" data-raw-source="[&lt;strong&gt;SURFOBJ&lt;/strong&gt;](/windows/win32/api/winddi/ns-winddi-_surfobj)"><strong>SURFOBJ</strong></a></p></td>
<td align="left"><p>标识图面，图面可以是 GDI 位图、设备相关位图或设备管理的图面。 有关详细信息，请参阅 <a href="surface-types.md" data-raw-source="[Surface Types](surface-types.md)">表面类型</a> 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/previous-versions/windows/hardware/drivers/ff570618(v=vs.85)" data-raw-source="[&lt;strong&gt;XFORMOBJ&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff570618(v=vs.85))"><strong>XFORMOBJ</strong></a></p></td>
<td align="left"><p>描述任意线性二维转换，例如几何宽线条。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/ns-winddi-xlateobj" data-raw-source="[&lt;strong&gt;XLATEOBJ&lt;/strong&gt;](/windows/win32/api/winddi/ns-winddi-_xlateobj)"><strong>XLATEOBJ</strong></a></p></td>
<td align="left"><p>定义将源表面格式的像素转换为目标图面的格式所需的翻译。</p></td>
</tr>
</tbody>
</table>

 

