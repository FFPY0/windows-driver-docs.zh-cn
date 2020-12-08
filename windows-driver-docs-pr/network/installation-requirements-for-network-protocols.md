---
title: 网络协议的安装要求
description: 网络协议的安装要求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d2ec035ef6b324c50b8b37e75b0a7582dff4a07
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96795977"
---
# <a name="installation-requirements-for-network-protocols"></a>网络协议的安装要求





本主题概述了网络协议的安装要求。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">INF 文件部分</th>
<th align="left">状态</th>
<th align="left">注释</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="version-section-in-a-network-inf-file.md" data-raw-source="[Version Section](version-section-in-a-network-inf-file.md)">版本部分</a></p></td>
<td align="left"><p>必须</p></td>
<td align="left"><p><strong>类</strong>= NetTrans</p>
<p><strong>ClassGuid</strong>= {4D36E975-E325-11CE-BFC1-08002BE10318}</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="/windows-hardware/drivers/install/inf-sourcedisksnames-section" data-raw-source="[&lt;strong&gt;INF SourceDisksNames Section&lt;/strong&gt;](../install/inf-sourcedisksnames-section.md)"><strong>Inf SourceDisksNames 部分</strong></a>和<a href="/windows-hardware/drivers/install/inf-sourcedisksfiles-section" data-raw-source="[&lt;strong&gt;INF SourceDisksFiles Section&lt;/strong&gt;](../install/inf-sourcedisksfiles-section.md)"> <strong>inf SourceDisksFiles 部分</strong></a></p></td>
<td align="left"><p>必需的 if .。。</p></td>
<td align="left"><p>如果 INF 文件未与 Windows 2000 一起分发，则是必需的。 如果 INF 文件与 Windows 2000 一起分发，则必须在 "<strong>版本</strong>" 部分中指定<strong>LayoutFile</strong>项，并且不会使用<strong>SourceDisksNames</strong>和<strong>SourceDisksFiles</strong>部分。</p>
<p>无特定于网络的要求。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/install/inf-destinationdirs-section" data-raw-source="[&lt;strong&gt;INF DestinationDirs Section&lt;/strong&gt;](../install/inf-destinationdirs-section.md)"><strong>INF DestinationDirs 节</strong></a></p></td>
<td align="left"><p>必须</p></td>
<td align="left"><p>无特定于网络的要求。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="controlflags-section-in-a-network-inf-file.md" data-raw-source="[ControlFlags Section](controlflags-section-in-a-network-inf-file.md)">ControlFlags 部分</a></p></td>
<td align="left"><p>可选</p></td>
<td align="left"><p>无特定于网络的要求。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/install/inf-manufacturer-section" data-raw-source="[&lt;strong&gt;INF Manufacturer Section&lt;/strong&gt;](../install/inf-manufacturer-section.md)"><strong>INF Manufacturer 节</strong></a></p></td>
<td align="left"><p>必须</p></td>
<td align="left"><p>无特定于网络的要求。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="models-section-in-a-network-inf-file.md" data-raw-source="[Models Section](models-section-in-a-network-inf-file.md)">模型部分</a></p></td>
<td align="left"><p>必须</p></td>
<td align="left"><p><em>Hw id</em>应该包含提供程序名称，后跟下划线和制造商名称或产品名称，例如： MS_DLC。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="ddinstall-section-in-a-network-inf-file.md" data-raw-source="[DDInstall Section](ddinstall-section-in-a-network-inf-file.md)">DDInstall 部分</a></p></td>
<td align="left"><p>必须</p></td>
<td align="left"><p><strong>特征</strong> 条目</p>
<p>允许的值：</p>
<p>NCF_HIDDEN</p>
<p>NCF_NO_SERVICE</p>
<p>NCF_NOT_USER_REMOVABLE</p>
<p>NCF_HAS_UI</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="ddinstall-services-section-in-a-network-inf-file.md" data-raw-source="[DDInstall.Services Section](ddinstall-services-section-in-a-network-inf-file.md)">DDInstall 部分</a></p></td>
<td align="left"><p>可选</p></td>
<td align="left"><p>无特定于网络的要求。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="add-registry-sections-in-a-network-inf-file.md" data-raw-source="[Add-registry-sections](add-registry-sections-in-a-network-inf-file.md)">添加-注册表-部分</a></p></td>
<td align="left"><p>必须</p></td>
<td align="left"><p>必需：</p>
<p>创建 Ndi 键</p>
<p><a href="specifying-binding-interfaces.md" data-raw-source="[Specifying Binding Interfaces](specifying-binding-interfaces.md)">指定绑定接口</a></p>
<p>允许的绑定接口：</p>
<p><strong>UpperRange</strong>：</p>
<p>netbios、ipx、tdi、winsock、noupper</p>
<p><strong>LowerRange</strong>：</p>
<p>ndis5, ndisatm, nolower</p></td>
</tr>
<tr class="even">
<td align="left"></td>
<td align="left"><p>可选</p></td>
<td align="left"><p><a href="setting-static-parameters.md" data-raw-source="[Setting static parameters for the component](setting-static-parameters.md)">为组件设置静态参数</a></p>
<p><a href="requiring-the-installation-of-another-network-component.md" data-raw-source="[Requiring the Installation of Another Network Component](requiring-the-installation-of-another-network-component.md)">要求安装另一个网络组件</a></p>
<p><a href="adding-service-related-values-to-the-ndi-key.md" data-raw-source="[Specifying service-related values](adding-service-related-values-to-the-ndi-key.md)">指定服务相关值</a></p>
<p><a href="adding-a-helptext-value.md" data-raw-source="[Adding a HelpText Value](adding-a-helptext-value.md)">添加 HelpText 值</a></p>
<p><a href="adding-registry-values-for-a-notify-object.md" data-raw-source="[Adding Registry Values for a Notify Object](adding-registry-values-for-a-notify-object.md)">添加通知对象的注册表值</a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="remove-section-in-a-network-inf-file.md" data-raw-source="[Remove Section](remove-section-in-a-network-inf-file.md)">删除节</a></p></td>
<td align="left"><p>可选</p></td>
<td align="left"></td>
</tr>
<tr class="even">
<td align="left"><p><a href="winsock-sections-in-a-network-inf-file.md" data-raw-source="[Winsock Sections](winsock-sections-in-a-network-inf-file.md)">Winsock 部分</a></p></td>
<td align="left"><p>可选</p></td>
<td align="left"><p>对于提供 Winsock 接口的协议，需要使用 <strong>winsock 安装</strong> 部分，并且 <strong>winsock-remove</strong> 部分是可选的。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="/windows-hardware/drivers/install/inf-strings-section" data-raw-source="[&lt;strong&gt;INF Strings Section&lt;/strong&gt;](../install/inf-strings-section.md)"><strong>INF Strings 节</strong></a></p></td>
<td align="left"><p>必须</p></td>
<td align="left"><p>无特定于网络的要求。</p></td>
</tr>
</tbody>
</table>

 

