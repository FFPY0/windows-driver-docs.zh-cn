---
title: 标准选项
description: 标准选项与标准功能关联，并由 GPD 语言识别的预定义名称标识。
keywords:
- 打印机选项 WDK Unidrv，standard
- 标准选项 WDK Unidrv
ms.date: 01/30/2018
ms.localizationpriority: medium
ms.openlocfilehash: 2b86919b58d94dd1f84901592a434c4d4cb07890
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806875"
---
# <a name="standard-options"></a>标准选项


标准选项是与 [标准功能](standard-features.md)关联的选项。 它们由 GPD 语言识别的预定义名称标识。 表示这些名称的字符串的资源标识符包含在 stdnames 中，gpd 由 Microsoft Windows 驱动程序工具包 (WDK) 提供。 

> [!IMPORTANT]
> 此资源可能在某些语言和国家/地区不可用。

下表列出了每个标准功能允许使用的标准选项名称。 使用这些名称作为 **\* 选项** 条目的参数。 包含打印架构选项关键字的功能是自动映射到打印架构选项关键字的选项名称。 还可以使用 **PrintSchemaKeywordMap** 属性将 GPD 选项映射为手动打印架构关键字。 打印架构记录在 Microsoft Windows SDK。

<table>
    <tbody>
        <tr>
            <td><b>功能名称</b></td>
            <td><b>标准选项名称</b></td>
            <td><b>默认打印架构选项关键字</b></td>
            <td><b>允许自定义选项？</b></td>
        </tr>
        <tr>
            <td><b>逐份打印</b></td>
            <td>OFF<br>ON</td>
            <td>彩色<br>排序</td>
            <td>否</td>
        </tr>
        <tr>
            <td><b>ColorMode</b></td>
            <td colspan="2">无标准选项</td>
            <td>是<br>另请参阅 <a href="/windows-hardware/drivers/print/handling-color-formats">处理颜色格式</a> 和 <a href="/windows-hardware/drivers/print/controlling-image-quality">控制图像质量</a>。</td>
        </tr>
        <tr>
            <td><b>双工</b></td>
            <td>横坐标<br>垂直<br>无</td>
            <td>TwoSidedShortEdge<br>TwoSidedLongEdge<br>OneSided</td>
            <td>否</td>
        </tr>
        <tr>
            <td><b>色</b></td>
            <td colspan="2">HT_PATSIZE_2x2<br>HT_PATSIZE_2x2_M<br>HT_PATSIZE_4x4<br>HT_PATSIZE_4x4_M<br>HT_PATSIZE_6x6<br>HT_PATSIZE_6x6_M<br>HT_PATSIZE_8x8<br>HT_PATSIZE_8x8_M<br>HT_PATSIZE_10x10<br>HT_PATSIZE_10x10_M<br>HT_PATSIZE_12x12<br>HT_PATSIZE_12x12_M<br>HT_PATSIZE_14x14<br>HT_PATSIZE_14x14_M<br>HT_PATSIZE_16x16<br>HT_PATSIZE_16x16_M<br>HT_PATSIZE_SUPERCELL<br>HT_PATSIZE_SUPERCELL_M<br>HT_PATSIZE_AUTO</td>
            <td>是<br>另请参阅 <a href="/windows-hardware/drivers/print/halftoning-with-unidrv">Unidrv 的半色调</a>。</td>
        </tr>
        <tr>
            <td rowspan="5"><b>InputBin</b></td>
            <td>AUTO<br>送<br>ENVFEED<br>ENVMANUAL</td>
            <td>送</td>
            <td rowspan="5">是</td>
        </tr>
        <tr>
            <td>FORMSOURCE</td>
            <td>AutoSelect</td>
        </tr>
        <tr>
            <td>LARGECAPACITY<br>LARGEFMT<br>LOWER</td>
            <td>高</td>
        </tr>
        <tr>
            <td>MANUAL<br>过程<br>SMALLFMT</td>
            <td>手动</td>
        </tr>
        <tr>
            <td>车<br>UPPER</td>
            <td>车</td>
        </tr>
        <tr>
            <td><b>MediaType</b></td>
            <td>镜面<br>STANDARD<br>透明化</td>
            <td>PhotographicGlossy<br>普通<br>透明度</td>
            <td>是<br>另请参阅 <a href="/windows-hardware/drivers/print/controlling-image-quality">控制图像质量</a>。</td>
        </tr>
        <tr>
            <td><b>内存</b></td>
            <td colspan="2">无标准选项</td>
            <td>是</td>
        </tr>
        <tr>
            <td><b>方向</b></td>
            <td>沿<br>LANDSCAPE_CC90<br>LANDSCAPE_CC270<br><br>有关后两个选项的详细信息，请参阅 <a href="/windows-hardware/drivers/print/specifying-paper-orientation">指定纸张方向</a>。</td>
            <td>纵向<br>横向<br>ReverseLandscape</td>
            <td>否</td>
        </tr>
        <tr>
            <td><b>PageProtect</b></td>
            <td colspan="2">ON<br>OFF</td>
            <td>否</td>
        </tr>
        <tr>
            <td rowspan="29"><b>PaperSize</b></td>
            <td>10X11<br>10X14<br>英寸</td>
            <td>NorthAmerica10x11<br>NorthAmerica10x14<br>NorthAmerica11x17</td>
            <td rowspan="29">是<br><b>注意</b>自定义名称不能超过<b>wingdi</b>中<b>CCHFORMNAME</b>指定的长度。</td>
        </tr>
        <tr>
            <td colspan="2">12X11<br>15X11</td>
        </tr>
        <tr>
            <td>9X11<br>A_PLUS</td>
            <td>NorthAmerica9x11<br>NorthAmericaSuperA</td>
        </tr>
        <tr>
            <td>A2<br>A3</td>
            <td>ISOA2<br>ISOA3</td>
        </tr>
        <tr>
            <td>A3_EXTRA<br>A3_EXTRA_TRANSVERSE</td>
            <td>ISOA3Extra</td>
        </tr>
        <tr>
            <td>A3_ROTATED<br>A3_TRANSVERSE</td>
            <td>ISOA3Rotated</td>
        </tr>
        <tr>
            <td>A4<br>A4_EXTRA<br>A4_PLUS</td>
            <td>ISOA4<br>ISOA4Extra<br>OtherMetricA4Plus</td>
        </tr>
        <tr>
            <td>A4_ROTATED<br>A4_TRANSVERSE</td>
            <td>ISOA4Rotated</td>
        </tr>
        <tr>
            <td colspan="2">A4SMALL</td>
        </tr>
        <tr>
            <td>A5<br>A5_EXTRA</td>
            <td>ISOA5<br>ISOA5Extra</td>
        </tr>
        <tr>
            <td>A5_ROTATED<br>A5_TRANSVERSE</td>
            <td>ISOA5Rotated</td>
        </tr>
        <tr>
            <td>A6<br>A6_ROTATED<br>B_PLUS<br>B4<br>B4_JIS_ROTATED<br>B5<br>B5_EXTRA</td>
            <td>ISOA6<br>ISOA6Rotated<br>NorthAmericaSuperB<br>JISB4<br>JISB4Rotated<br>JISB5<br>ISOB5Extra</td>
        </tr>
        <tr>
            <td>B5_JIS_ROTATED<br>B5_TRANSVERSE</td>
            <td>JISB5Rotated</td>
        </tr>
        <tr>
            <td>B6_JIS<br>B6_JIS_ROTATED</td>
            <td>JISB6<br>JISB6Rotated</td>
        </tr>
        <tr>
            <td>CSHEET<br>CUSTOMSIZE</td>
            <td>NorthAmericaCSheet</td>
        </tr>
        <tr>
            <td>DBL_JAPANESE_POSTCARD<br>DBL_JAPANESE_POSTCARD_ROTATED<br>DSHEET<br>ENV_10<br>ENV_11<br>ENV_12<br>ENV_14<br>ENV_9<br>ENV_B4<br>ENV_B5</td>
            <td>JapanDoubleHagakiPostcard<br>JapanDoubleHagakiPostcardRotated<br>NorthAmericaDSheet<br>NorthAmericaNumber10Envelope<br>NorthAmericaNumber11Envelope<br>NorthAmericaNumber12Envelope<br>NorthAmericaNumber14Envelope<br>NorthAmericaNumber9Envelope<br>ISOB4Envelope<br>ISOB5Envelope</td>
        </tr>
        <tr>
            <td colspan="2">ENV_B6</td>
        </tr>
        <tr>
            <td>ENV_C3<br>ENV_C4<br>ENV_C5<br>ENV_C6<br>ENV_C65<br>ENV_DL<br>ENV_INVITE<br>ENV_ITALY<br>ENV_MONARCH<br>ENV_PERSONAL<br>ESHEET<br>人员<br>FANFOLD_LGL_GERMAN</td>
            <td>ISOC3Envelope<br>ISOC4Envelope<br>ISOC5Envelope<br>ISOC6Envelope<br>ISOC6C5Envelope<br>ISODLEnvelope<br>OtherMetricInviteEnvelope<br>OtherMetricItalianEnvelope<br>NorthAmericaMonarchEnvelope<br>NorthAmericaPersonalEnvelope<br>NorthAmericaESheet<br>NorthAmericaExecutive<br>NorthAmericaGermanLegalFanfold</td>
        </tr>
        <tr>
            <td>FANFOLD_STD_GERMAN<br>FANFOLD_US</td>
            <td>NorthAmericaGermanStandardFanfold</td>
        </tr>
        <tr>
            <td>对开<br>ISO_B4<br>JAPANESE_POSTCARD<br>JAPANESE_POSTCARD_ROTATED<br>JENV_CHOU3<br>JENV_CHOU3_ROTATED<br>JENV_CHOU4<br>JENV_CHOU4_ROTATED<br>JENV_KAKU2<br>JENV_KAKU2_ROTATED<br>JENV_KAKU3<br>JENV_KAKU3_ROTATED<br>JENV_YOU4<br>JENV_YOU4_ROTATED</td>
            <td>OtherMetricFolio<br>ISOB4<br>JapanHagakiPostcard<br>JapanHagakiPostcardRotated<br>JapanChou3Envelope<br>JapanChou3EnvelopeRotated<br>JapanChou4Envelope<br>JapanChou4EnvelopeRotated<br>JapanKaku2Envelope<br>JapanKaku2EnvelopeRotated<br>JapanKaku3Envelope<br>JapanKaku3EnvelopeRotated<br>JapanYou4Envelope<br>JapanYou4EnvelopeRotated</td>
        </tr>
        <tr>
            <td colspan="2">LEDGER</td>
        </tr>
        <tr>
            <td>法规<br>LEGAL_EXTRA<br>驱动器</td>
            <td>NorthAmericaLegal<br>NorthAmericaLegalExtra<br>NorthAmericaLetter</td>
        </tr>
        <tr>
            <td>LETTER_EXTRA<br>LETTER_EXTRA_TRANSVERSE</td>
            <td>NorthAmericaLetterExtra</td>
        </tr>
        <tr>
            <td>LETTER_PLUS</td>
            <td>NorthAmericaLetterPlus</td>
        </tr>
        <tr>
            <td>LETTER_ROTATED<br>LETTER_TRANSVERSE</td>
            <td>NorthAmericaLetterRotated</td>
        </tr>
        <tr>
            <td colspan="2">LETTERSMALL</td>
        </tr>
        <tr>
            <td>注意<br>P16K<br>P16K_ROTATED<br>P32K<br>P32K_ROTATED</td>
            <td>NorthAmericaNote<br>PRC16K<br>PRC16KRotated<br>PRC32K<br>PRC32KRotated</td>
        </tr>
        <tr>
            <td>P32KBIG<br>P32KBIG_ROTATED</td>
            <td>PRC32KBig</td>
        </tr>
        <tr>
            <td>PENV_1<br>PENV_1_ROTATED<br>PENV_10<br>PENV_10_ROTATED<br>PENV_2<br>PENV_2_ROTATED<br>PENV_3<br>PENV_3_ROTATED<br>PENV_4<br>PENV_4_ROTATED<br>PENV_5<br>PENV_5_ROTATED<br>PENV_6<br>PENV_6_ROTATED<br>PENV_7<br>PENV_7_ROTATED<br>PENV_8<br>PENV_8_ROTATED<br>PENV_9<br>PENV_9_ROTATED<br>四开<br>STATEMENT<br>纸<br>TABLOID_EXTRA</td>
            <td>PRC1Envelope<br>PRC1EnvelopeRotated<br>PRC10Envelope<br>PRC10EnvelopeRotated<br>PRC2Envelope<br>PRC2EnvelopeRotated<br>PRC3Envelope<br>PRC3EnvelopeRotated<br>PRC4Envelope<br>PRC4EnvelopeRotated<br>PRC5Envelope<br>PRC5EnvelopeRotated<br>PRC6Envelope<br>PRC6EnvelopeRotated<br>PRC7Envelope<br>PRC7EnvelopeRotated<br>PRC8Envelope<br>PRC8EnvelopeRotated<br>PRC9Envelope<br>PRC9EnvelopeRotated<br>NorthAmericaQuarto<br>NorthAmericaStatement<br>NorthAmericaTabloid<br>NorthAmericaTabloidExtra</td>
        </tr>
        <tr>
            <td><b>解决方法</b></td>
            <td colspan="2">无标准选项</td>
            <td>是</td>
        </tr>
    </tbody>
</table>


## <a name="related-topics"></a>相关主题


[控制图像质量](controlling-image-quality.md)  
[使用 Unidrv 设置半色调](halftoning-with-unidrv.md)  
[指定纸张方向](specifying-paper-orientation.md)  
[标准功能](standard-features.md)
