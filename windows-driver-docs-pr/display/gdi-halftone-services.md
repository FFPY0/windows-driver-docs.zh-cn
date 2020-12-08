---
title: GDI 半色调服务
description: GDI 半色调服务
keywords:
- GDI WDK Windows 2000 显示，半色调
- 图形驱动程序 WDK Windows 2000 显示，半色调
- 绘制 WDK GDI，半色调
- 半色调 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3c66d1ba0333cdc85d7e00c00660d4972dc1ea4e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96798313"
---
# <a name="gdi-halftone-services"></a>GDI 半色调服务


## <span id="ddk_gdi_halftone_services_gg"></span><span id="DDK_GDI_HALFTONE_SERVICES_GG"></span>


GDI 半色调支持包括下表中列出的服务。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">函数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-ht_computergbgammatable" data-raw-source="[&lt;strong&gt;HT_ComputeRGBGammaTable&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-ht_computergbgammatable)"><strong>HT_ComputeRGBGammaTable</strong></a></p></td>
<td align="left"><p>使 GDI 基于伽玛数字计算设备的红色、绿色和蓝色浓度。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-ht_get8bppformatpalette" data-raw-source="[&lt;strong&gt;HT_Get8BPPFormatPalette&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-ht_get8bppformatpalette)"><strong>HT_Get8BPPFormatPalette</strong></a></p></td>
<td align="left"><p>返回一个半色调调色板，用于每像素标准8位设备类型。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-ht_get8bppmaskpalette" data-raw-source="[&lt;strong&gt;HT_Get8BPPMaskPalette&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-ht_get8bppmaskpalette)"><strong>HT_Get8BPPMaskPalette</strong></a></p></td>
<td align="left"><p>返回8位/像素设备类型的掩码调色板。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows/win32/api/winddi/nf-winddi-htui_devicecoloradjustment" data-raw-source="[&lt;strong&gt;HTUI_DeviceColorAdjustment&lt;/strong&gt;](/windows/win32/api/winddi/nf-winddi-htui_devicecoloradjustment)"><strong>HTUI_DeviceColorAdjustment</strong></a></p></td>
<td align="left"><p>显示允许用户调整设备的半色调属性的对话框。</p></td>
</tr>
</tbody>
</table>

 

