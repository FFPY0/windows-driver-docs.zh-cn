---
title: 重命名的 WHEA 数据类型
description: 重命名的 WHEA 数据类型
keywords:
- Windows 硬件错误体系结构 WDK，已重命名数据类型
- WHEA WDK，已重命名数据类型
- 硬件错误 WDK WHEA，已重命名数据类型
- 重命名数据类型 WDK WHEA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c49c4e22a36b1880b1f0eaa0c29dd1f578288ab7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96804323"
---
# <a name="renamed-whea-data-types"></a>重命名的 WHEA 数据类型


从 Windows 7 Windows 驱动程序工具包开始 (WDK) ，各种 WHEA 数据类型已从 WDK 的早期版本重命名。 进行大多数更改是为了使 WDK 中的命名约定与 *常见平台错误记录* 格式的命名约定保持一致。 [统一可扩展固件接口 (UEFI) 规范](https://go.microsoft.com/fwlink/p/?linkid=69484)的版本2.2 的附录 N 中描述了此格式。

此部分中列出的数据类型尚未针对 Windows 7 进行修订。 例如，在重命名的结构中，成员的列表和类型也不会发生更改，不过成员本身可能已被重命名。

如果要 [ (PSHED) 插件开发新的特定于平台的硬件错误驱动程序](platform-specific-hardware-error-driver-plug-ins2.md)，请使用 Windows 7 和更高版本中定义的新 WHEA 数据类型名称。

如果你正在使用 Windows 7 和更高版本的 WDK 构建现有的 PSHED 插件，你仍可以使用以前的 WHEA 数据类型名称。 为此，请将以下内容添加到用于生成插件的 *源文件* 中：

`C_DEFINES = $(C_DEFINES) /DWHEA_DOWNLEVEL_TYPE_NAMES`

但对于现有的 PSHED 插件，强烈建议使用 Windows 7 和更高版本的 WDK 中定义的名称重命名 WHEA 数据类型。

下表列出了 WHEA 数据类型 "以前的" 和新的名称。

### <a name="renamed-whea-globally-unique-identifiers-guids"></a><a href="" id="renamed-whea-globally-unique-identifiers--guids-"></a> 已重命名 WHEA Globally-Unique 标识符 (Guid) 

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Windows 7 之前的版本 (WDK 版本) </th>
<th>Windows 7 WDK 和更高版本 (的新名称) </th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>IPF_PROCESSOR_SPECIFIC_SECTION_GUID</p></td>
<td><p>IPF_PROCESSOR_ERROR_SECTION_GUID</p></td>
</tr>
<tr class="even">
<td><p>IPF_SAL_RECORD_REFERENCE_SECTION_GUID</p></td>
<td><p>FIRMWARE_ERROR_RECORD_REFERENCE_GUID</p></td>
</tr>
<tr class="odd">
<td><p>PCIEXPRESS_SECTION_GUID</p></td>
<td><p>PCIEXPRESS_ERROR_SECTION_GUID</p></td>
</tr>
<tr class="even">
<td><p>PCIX_BUS_SECTION_GUID</p></td>
<td><p>PCIXBUS_ERROR_SECTION_GUID</p></td>
</tr>
<tr class="odd">
<td><p>PCIX_COMPONENT_SECTION_GUID</p></td>
<td><p>PCIXBUS_ERROR_SECTION_GUID</p></td>
</tr>
<tr class="even">
<td><p>PLATFORM_MEMORY_SECTION_GUID</p></td>
<td><p>MEMORY_ERROR_SECTION_GUID</p></td>
</tr>
<tr class="odd">
<td><p>PROCESSOR_GENERIC_SECTION_GUID</p></td>
<td><p>PROCESSOR_GENERIC_ERROR_SECTION_GUID</p></td>
</tr>
<tr class="even">
<td><p>X86_PROCESSOR_SPECIFIC_SECTION_GUID</p></td>
<td><p>XPF_PROCESSOR_ERROR_SECTION_GUID</p></td>
</tr>
</tbody>
</table>

 

### <a name="renamed-whea-defines"></a><a href="" id="renamed-whea-defines"></a> 重命名的 WHEA 定义

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Windows 7 之前的版本 (WDK 版本) </th>
<th>Windows 7 WDK 和更高版本 (的新名称) </th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WHEA_SECTION_DESCRIPTOR_REVISION</p></td>
<td><p>WHEA_ERROR_RECORD_SECTION_DESCRIPTOR_REVISION</p></td>
</tr>
</tbody>
</table>

 

### <a name="renamed-whea-structures-and-unions"></a><a href="" id="renamed-whea-structures-and-unions"></a> 已重命名 WHEA 结构和联合

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>Windows 7 之前的版本 (WDK 版本) </th>
<th>Windows 7 WDK 和更高版本 (的新名称) </th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>WHEA_FIRMWARE_RECORD</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_firmware_error_record_reference" data-raw-source="[&lt;strong&gt;WHEA_FIRMWARE_ERROR_RECORD_REFERENCE&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_firmware_error_record_reference)"><strong>WHEA_FIRMWARE_ERROR_RECORD_REFERENCE</strong></a></p></td>
</tr>
<tr class="even">
<td><p>WHEA_GENERIC_PROCESSOR_ERROR</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_processor_generic_error_section" data-raw-source="[&lt;strong&gt;WHEA_PROCESSOR_GENERIC_ERROR_SECTION&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_processor_generic_error_section)"><strong>WHEA_PROCESSOR_GENERIC_ERROR_SECTION</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>WHEA_GENERIC_PROCESSOR_ERROR_VALIDBITS</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_processor_generic_error_section_validbits" data-raw-source="[&lt;strong&gt;WHEA_PROCESSOR_GENERIC_ERROR_SECTION_VALIDBITS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_processor_generic_error_section_validbits)"><strong>WHEA_PROCESSOR_GENERIC_ERROR_SECTION_VALIDBITS</strong></a></p></td>
</tr>
<tr class="even">
<td><p>WHEA_MEMORY_ERROR</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_memory_error_section" data-raw-source="[&lt;strong&gt;WHEA_MEMORY_ERROR_SECTION&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_memory_error_section)"><strong>WHEA_MEMORY_ERROR_SECTION</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>WHEA_MEMORY_ERROR_VALIDBITS</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_memory_error_section_validbits" data-raw-source="[&lt;strong&gt;WHEA_MEMORY_ERROR_SECTION_VALIDBITS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_memory_error_section_validbits)"><strong>WHEA_MEMORY_ERROR_SECTION_VALIDBITS</strong></a></p></td>
</tr>
<tr class="even">
<td><p>WHEA_NMI_ERROR</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_nmi_error_section" data-raw-source="[&lt;strong&gt;WHEA_NMI_ERROR_SECTION&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_nmi_error_section)"><strong>WHEA_NMI_ERROR_SECTION</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>WHEA_PCIEXPRESS_ERROR</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_pciexpress_error_section" data-raw-source="[&lt;strong&gt;WHEA_PCIEXPRESS_ERROR_SECTION&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_pciexpress_error_section)"><strong>WHEA_PCIEXPRESS_ERROR_SECTION</strong></a></p></td>
</tr>
<tr class="even">
<td><p>WHEA_PCIEXPRESS_ERROR_VALIDBITS</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_pciexpress_error_section_validbits" data-raw-source="[&lt;strong&gt;WHEA_PCIEXPRESS_ERROR_SECTION_VALIDBITS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_pciexpress_error_section_validbits)"><strong>WHEA_PCIEXPRESS_ERROR_SECTION_VALIDBITS</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>WHEA_PCIXBUS_ERROR</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_pcixbus_error_section" data-raw-source="[&lt;strong&gt;WHEA_PCIXBUS_ERROR_SECTION&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_pcixbus_error_section)"><strong>WHEA_PCIXBUS_ERROR_SECTION</strong></a></p></td>
</tr>
<tr class="even">
<td><p>WHEA_PCIXBUS_ERROR_VALIDBITS</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_pcixbus_error_section_validbits" data-raw-source="[&lt;strong&gt;WHEA_PCIXBUS_ERROR_SECTION_VALIDBITS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_pcixbus_error_section_validbits)"><strong>WHEA_PCIXBUS_ERROR_SECTION_VALIDBITS</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>WHEA_PCIXDEVICE_ERROR</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_pcixdevice_error_section" data-raw-source="[&lt;strong&gt;WHEA_PCIXDEVICE_ERROR_SECTION&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_pcixdevice_error_section)"><strong>WHEA_PCIXDEVICE_ERROR_SECTION</strong></a></p></td>
</tr>
<tr class="even">
<td><p>WHEA_PCIXDEVICE_ERROR_VALIDBITS</p></td>
<td><p><a href="/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_pcixdevice_error_section_validbits" data-raw-source="[&lt;strong&gt;WHEA_PCIXDEVICE_ERROR_SECTION_VALIDBITS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_whea_pcixdevice_error_section_validbits)"><strong>WHEA_PCIXDEVICE_ERROR_SECTION_VALIDBITS</strong></a></p></td>
</tr>
<tr class="odd">
<td><p>WHEA_XPF_PROCESSOR_ERROR</p></td>
<td><p><a href="/previous-versions/ff560655(v=vs.85)" data-raw-source="[&lt;strong&gt;WHEA_XPF_PROCESSOR_ERROR_SECTION&lt;/strong&gt;](/previous-versions/ff560655(v=vs.85))"><strong>WHEA_XPF_PROCESSOR_ERROR_SECTION</strong></a></p></td>
</tr>
<tr class="even">
<td><p>WHEA_XPF_PROCESSOR_ERROR_VALIDBITS</p></td>
<td><p><a href="/previous-versions/ff560657(v=vs.85)" data-raw-source="[&lt;strong&gt;WHEA_XPF_PROCESSOR_ERROR_SECTION_VALIDBITS&lt;/strong&gt;](/previous-versions/ff560657(v=vs.85))"><strong>WHEA_XPF_PROCESSOR_ERROR_SECTION_VALIDBITS</strong></a></p></td>
</tr>
</tbody>
</table>

 

