---
title: 生成已跳过的宏块
description: 生成已跳过的宏块
keywords:
- macroblocks WDK DirectX VA，跳过 macroblocks
- 已跳过 macroblocks WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 55e45fcaf835f28c7fbdaf0c6163d29425a9a6de
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803919"
---
# <a name="generating-skipped-macroblocks"></a>生成已跳过的宏块


## <span id="ddk_generating_skipped_macroblocks_gg"></span><span id="DDK_GENERATING_SKIPPED_MACROBLOCKS_GG"></span>


在 DirectX VA 中的已跳过宏块的生成与 MPEG-2 视频部分第7.6.6 中略有不同。 在 DirectX VA 中，跳过 macroblocks 是在单独的宏块控制命令中生成的，而不是从前面 nonskipped 宏块的类型推断出，而是从显示的图片类型 (例如，在 MPEG-2 中，生成跳过的 macroblocks 的方法取决于图片是 *P 图片* 还是 *B 图片*。 ) 

生成和使用跳过的 macroblocks 时，需要满足以下条件：

- 跳过的 macroblocks 没有剩余差额。

- 通过重复使用 **wMBaddress** 的宏块 control 命令的操作，可生成跳过的 macroblocks。  (以与第一个相同的方式生成每个后续跳过的宏块，但递增 **wMBaddress** 的值除外。 ) 

- 宏块跳过限制为图片中的 macroblocks 换行。  (必须发送单独的宏块 control 命令才能生成 macroblocks 的每一行的第一个宏块。 ) 

- *MBskipsFollowing* 的宏块控件命令的内容等效 (除了 *MBskipsFollowing* 的值) 到所跳过的 macroblocks 的第一个序列的内容中。 因此，当 *MBskipsFollowing* 不为零时，以下结构成员和变量必须都等于零： *Motion4MV、IntraMacroblock、* **wPatternCode**<em>和</em> **wPC \_ 溢出**。

由于前面三个条件，在 *Motion4MV* 为零时，加速器可以实现运动 (补偿) 方法是：将指定的运动向量应用到宽度等于以下表达式的宽度的矩形，并将其应用于色度组件中的类似指定矩形。 此矩形区域运动补偿方法可由加速器执行，而不是通过使用同一宏块控制操作的 *MBskipsFollowing*+ 1 重复来执行。

```cpp
(bMacroblockWidthMinus1+1) X (MBskipsFollowing+1)
```

**BMacroblockWidthMinus1** 成员包含在 [**DXVA \_ PictureParameters**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_pictureparameters)中。 *MBskipsFollowing* 变量位于每个宏块控制结构的 **wMBtype** 成员中。

### <a name="span-idskipped_macroblocks_in_h263__annex_f_spanspan-idskipped_macroblocks_in_h263__annex_f_spanspan-idskipped_macroblocks_in_h263__annex_f_spanskipped-macroblocks-in-h263-annex-f"></a><span id="Skipped_Macroblocks_in_H.263__Annex_F_"></span><span id="skipped_macroblocks_in_h.263__annex_f_"></span><span id="SKIPPED_MACROBLOCKS_IN_H.263__ANNEX_F_"></span>已跳过 Macroblocks 中的 (附录 F) 

在 macroblocks 中生成的已跳过的具有高级预测模式 (附录 F) ，要求在 DirectX VA 宏块控制命令中将某些已跳过的 macroblocks 作为 nonskipped macroblocks。 这样做是为了在这些 macroblocks 中生成 *OBMC* 效果。

### <a name="span-idgenerating_skipped_macroblocks_in_mpeg-2_examplespanspan-idgenerating_skipped_macroblocks_in_mpeg-2_examplespanspan-idgenerating_skipped_macroblocks_in_mpeg-2_examplespangenerating-skipped-macroblocks-in-mpeg-2-example"></a><span id="Generating_Skipped_Macroblocks_in_MPEG-2_Example"></span><span id="generating_skipped_macroblocks_in_mpeg-2_example"></span><span id="GENERATING_SKIPPED_MACROBLOCKS_IN_MPEG-2_EXAMPLE"></span>在 MPEG-2 示例中生成跳过的 Macroblocks

下面的示例说明了在生成跳过 macroblocks 时如何使用宏块控件命令。 出于演示目的，假设在 MPEG-2 位流 7 macroblocks 中按以下方式使用。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">宏块号</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0</p></td>
<td align="left"><p>用残差编码</p></td>
</tr>
<tr class="even">
<td align="left"><p>1</p></td>
<td align="left"><p>已跳过</p></td>
</tr>
<tr class="odd">
<td align="left"><p>2</p></td>
<td align="left"><p>用残差编码</p></td>
</tr>
<tr class="even">
<td align="left"><p>3</p></td>
<td align="left"><p>已跳过</p></td>
</tr>
<tr class="odd">
<td align="left"><p>4</p></td>
<td align="left"><p>已跳过</p></td>
</tr>
<tr class="even">
<td align="left"><p>5</p></td>
<td align="left"><p>已跳过</p></td>
</tr>
<tr class="odd">
<td align="left"><p>6</p></td>
<td align="left"><p>用残差编码</p></td>
</tr>
</tbody>
</table>

 

这七个 macroblocks 要求代 (至少) 下表中所示的五个 DirectX VA 宏块控制命令。 *MBskipsFollowing* 变量指示跳过的 macroblocks 数。 **WMBaddress** 成员指示宏块的地址。 *MBskipsFollowing* 和 **WMBaddress** 包含在 [**DXVA \_ MBctrl \_ p \_ OffHostIDCT \_ 1**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mbctrl_p_offhostidct_1)和 [**DXVA \_ MBctrl \_ p \_ HostResidDiff \_ 1**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_mbctrl_p_hostresiddiff_1) 结构中。  (在 **dwMB \_ SNL** 结构成员中定义 *MBskipsFollowing* 变量。 ) 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">宏块命令</th>
<th align="left">成员值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>First</p></td>
<td align="left"><p><strong>wMBaddress</strong> = 0</p>
<p><em>MBskipsFollowing</em> = 0</p></td>
</tr>
<tr class="even">
<td align="left"><p>秒</p></td>
<td align="left"><p><strong>wMBaddress</strong> = 1</p>
<p><em>MBskipsFollowing</em> = 0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>第三个</p></td>
<td align="left"><p><strong>wMBaddress</strong> = 2</p>
<p><em>MBskipsFollowing</em> = 0</p></td>
</tr>
<tr class="even">
<td align="left"><p>第四个</p></td>
<td align="left"><p><strong>wMBaddress</strong> = 3</p>
<p><em>MBskipsFollowing</em> = 2</p></td>
</tr>
<tr class="odd">
<td align="left"><p>第五个</p></td>
<td align="left"><p><strong>wMBaddress</strong> = 6</p>
<p><em>MBskipsFollowing</em> = 0</p></td>
</tr>
</tbody>
</table>

 

 

