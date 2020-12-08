---
title: IPrintOemUI COM 接口
description: IPrintOemUI COM 接口
keywords:
- IPrintOemUI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 806067a743523764e98f5a803c7d08c57d7bd923
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96796549"
---
# <a name="iprintoemui-com-interface"></a>IPrintOemUI COM 接口





`IPrintOemUI`COM 接口是 Unidrv 或 Pscript5 的[打印机接口 DLL](printer-interface-dll.md)与 UI 插件通信的方式。 `IPrintOemUI`接口由每个 UI 插件实现。

下表列出并描述了接口提供的所有方法 `IPrintOemUI` 。 UI 插件必须定义所有列出的方法。 如果方法不是必需的，则可以只返回 E \_ NOTIMPL。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>方法</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-commonuiprop" data-raw-source="[&lt;strong&gt;IPrintOemUI::CommonUIProp&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-commonuiprop)"><strong>IPrintOemUI::CommonUIProp</strong></a></p></td>
<td><p>启用 UI 插件来修改现有打印机属性表页或文档属性表页。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-devicecapabilities" data-raw-source="[&lt;strong&gt;IPrintOemUI::DeviceCapabilities&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-devicecapabilities)"><strong>IPrintOemUI：:D eviceCapabilities</strong></a></p></td>
<td><p>允许 UI 插件指定自定义的设备功能。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-devicepropertysheets" data-raw-source="[&lt;strong&gt;IPrintOemUI::DevicePropertySheets&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-devicepropertysheets)"><strong>IPrintOemUI：:D evicePropertySheets</strong></a></p></td>
<td><p>启用 UI 插件以将新页面添加到打印机设备的打印机属性表。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-devmode" data-raw-source="[&lt;strong&gt;IPrintOemUI::DevMode&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-devmode)"><strong>IPrintOemUI：:D evMode</strong></a></p></td>
<td><p>对 UI 插件的私有 <a href="/windows/win32/api/wingdi/ns-wingdi-devmodew" data-raw-source="[&lt;strong&gt;DEVMODEW&lt;/strong&gt;](/windows/win32/api/wingdi/ns-wingdi-devmodew)"><strong>DEVMODEW</strong></a> 成员执行操作。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-devqueryprintex" data-raw-source="[&lt;strong&gt;IPrintOemUI::DevQueryPrintEx&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-devqueryprintex)"><strong>IPrintOemUI：:D evQueryPrintEx</strong></a></p></td>
<td><p>启用 UI 插件以帮助确定打印作业是否可打印。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-documentpropertysheets" data-raw-source="[&lt;strong&gt;IPrintOemUI::DocumentPropertySheets&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-documentpropertysheets)"><strong>IPrintOemUI：:D ocumentPropertySheets</strong></a></p></td>
<td><p>允许 UI 插件向打印机设备的文档属性表添加新页。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-driverevent" data-raw-source="[&lt;strong&gt;IPrintOemUI::DriverEvent&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-driverevent)"><strong>IPrintOemUI：:D riverEvent</strong></a></p></td>
<td><p>当处理驱动程序特定的事件时，打印后台处理程序会调用这些事件，这些事件可能需要打印机驱动程序的操作。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-fontinstallerdlgproc" data-raw-source="[&lt;strong&gt;IPrintOemUI::FontInstallerDlgProc&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-fontinstallerdlgproc)"><strong>IPrintOemUI::FontInstallerDlgProc</strong></a></p></td>
<td><p>替换 Unidrv 字体安装程序的用户界面。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-getinfo" data-raw-source="[&lt;strong&gt;IPrintOemUI::GetInfo&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-getinfo)"><strong>IPrintOemUI：： GetInfo</strong></a></p></td>
<td><p>需要 (实现。 ) 返回 UI 插件的标识信息。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-printerevent" data-raw-source="[&lt;strong&gt;IPrintOemUI::PrinterEvent&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-printerevent)"><strong>IPrintOemUI：:P rinterEvent</strong></a></p></td>
<td><p>启用 UI 插件来处理打印机事件。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-publishdriverinterface" data-raw-source="[&lt;strong&gt;IPrintOemUI::PublishDriverInterface&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-publishdriverinterface)"><strong>IPrintOemUI：:P ublishDriverInterface</strong></a></p></td>
<td><p>需要 (实现。 ) 提供一个指针，指向 Unidrv 或 Pscript5 驱动程序的 <a href="iprintoemdriverui-com-interface.md" data-raw-source="[IPrintOemDriverUI COM interface](iprintoemdriverui-com-interface.md)">IPRINTOEMDRIVERUI com 接口</a>， <a href="iprintcoreui2-com-interface.md" data-raw-source="[IPrintCoreUI2 COM interface](iprintcoreui2-com-interface.md)">IPrintCoreUI2 com 接口</a>， <a href="/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperps" data-raw-source="[IPrintCoreHelperPS interface](/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperps)">IPrintCoreHelperPS 接口</a>，或 <a href="/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperuni" data-raw-source="[IPrintCoreHelperUni interface](/windows-hardware/drivers/ddi/prcomoem/nn-prcomoem-iprintcorehelperuni)">IPrintCoreHelperUni 接口</a>。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-querycolorprofile" data-raw-source="[&lt;strong&gt;IPrintOemUI::QueryColorProfile&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-querycolorprofile)"><strong>IPrintOemUI::QueryColorProfile</strong></a></p></td>
<td><p>启用打印机接口 DLL 以指定用于颜色管理的 ICC 配置文件。</p></td>
</tr>
<tr class="odd">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-updateexternalfonts" data-raw-source="[&lt;strong&gt;IPrintOemUI::UpdateExternalFonts&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-updateexternalfonts)"><strong>IPrintOemUI::UpdateExternalFonts</strong></a></p></td>
<td><p>启用打印机接口 DLL 以更新打印机的 <a href="customized-font-management.md#ddk-unidrv-font-format-files-gg" data-raw-source="[Unidrv font format files](customized-font-management.md#ddk-unidrv-font-format-files-gg)">Unidrv 字体格式文件</a>。</p></td>
</tr>
<tr class="even">
<td><p><a href="/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-upgradeprinter" data-raw-source="[&lt;strong&gt;IPrintOemUI::UpgradePrinter&lt;/strong&gt;](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-upgradeprinter)"><strong>IPrintOemUI::UpgradePrinter</strong></a></p></td>
<td><p>启用 UI 插件来升级注册表中存储的设备选项值。</p></td>
</tr>
</tbody>
</table>

 

有关详细信息，请参阅 [实现打印机驱动程序 COM 接口](implementing-printer-driver-com-interfaces.md)。

