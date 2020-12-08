---
title: headerPath XML 元素
description: headerPath XML 元素
keywords:
- headerPath XML 元素设备和驱动程序安装
topic_type:
- apiref
api_name:
- headerPath XML Element
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 47ac105e351fa3a5fa42026f30f54a97830ea72f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791767"
---
# <a name="headerpath-xml-element"></a>headerPath XML 元素


\[DIFx 已弃用，有关详细信息，请参阅 [DIFx 指导原则](./difx-guidelines.md)。\]

**HeaderPath** XML 元素指定 DPInst 显示在 DPInst EULA 页和 DPInst 安装页右上角的自定义标头位图的源文件名。

### <a name="element-tag"></a>元素标记

```cpp
<headerPath>
```

### <a name="xml-attributes"></a>XML 属性

无

### <a name="element-information"></a>元素信息

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>父元素</strong></p></td>
<td align="left"><p><a href="dpinst-xml-element.md" data-raw-source="[&lt;strong&gt;dpinst&lt;/strong&gt;](dpinst-xml-element.md)"><strong>dpinst</strong></a>或<a href="language-xml-element.md" data-raw-source="[&lt;strong&gt;language&lt;/strong&gt;](language-xml-element.md)"> <strong>language</strong></a></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>子元素</strong></p></td>
<td align="left"><p>不允许</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>数据内容</strong></p></td>
<td align="left"><p>String，指定 DPInst 在 DPInst EULA 和安装页的右上角显示的标头位图的文件名。 标头位图文件必须位于 DPInst 根目录中，该目录包含 DPInst 可执行文件 (<em>DPInst.exe</em>) ，或位于 DPInst 根目录下的子目录中。 如果标头位图文件位于子目录中，请指定一个相对于 DPInst 根目录的完全限定文件名。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>重复的子元素</strong></p></td>
<td align="left"><p>不允许</p></td>
</tr>
</tbody>
</table>

 

### <a name="remarks"></a><a href="" id="comments"></a>注释

如果 **headerPath** 元素是 **dpinst** XML 元素的子元素，则对其进行自定义，但不本地化。 如果 **headerPath** 元素为 **language** XML 元素的子元素，则自定义并本地化该元素。

下面的代码示例演示了一个 **headerPath** 元素，该元素指定 *\\Header.bmp* 为 DPInst 显示在 DPInst EULA 和安装页和安装页右上角的标头位图文件的数据。 指定自定义标头位图文件的文本以粗体显示。

```cpp
<dpinst>
  ...
  <headerPath>Data\Header.bmp</headerPath>
  ...
</dpinst>
```

如果未指定 **headerPath** 元素，则 DPInst 将使用默认标头位图。

## <a name="see-also"></a>请参阅


[**dpinst**](dpinst-xml-element.md)

[**语言**](language-xml-element.md)

 

