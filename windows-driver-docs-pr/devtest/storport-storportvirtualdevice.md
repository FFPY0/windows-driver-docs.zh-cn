---
title: 'StorPortVirtualDevice 规则 (storport) '
description: 此规则验证在 HwStorFindAdapter 例程退出后，端口 \_ 配置信息 (Storport) 结构中的 "VirtualDevice" 字段 \_ 是否已设置为 "FALSE"。 此规则仅适用于物理 StorPort 微型端口。
ms.date: 05/21/2018
keywords:
- 'StorPortVirtualDevice 规则 (storport) '
topic_type:
- apiref
api_name:
- StorPortVirtualDevice
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 0325dab48095e6fe2c2ab2bc1517ac1ce72a2c99
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841281"
---
# <a name="storportvirtualdevice-rule-storport"></a>StorPortVirtualDevice 规则 (storport) 


此规则验证在 [**HwStorFindAdapter**](/windows-hardware/drivers/ddi/storport/nc-storport-hw_find_adapter)例程退出后，[**端口 \_ 配置 \_ 信息 (Storport)**](/previous-versions/windows/hardware/drivers/ff563901(v=vs.85))结构中的 " **VirtualDevice** " 字段是否已设置为 " **FALSE**"。 此规则仅适用于物理 StorPort 微型端口。

**驱动程序模型： Storport**

<a name="how-to-test"></a>如何测试
-----------

<table>
<colgroup>
<col width="100%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">在编译时</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>运行 <a href="/windows-hardware/drivers/devtest/static-driver-verifier" data-raw-source="[Static Driver Verifier](./static-driver-verifier.md)">静态驱动程序验证程序</a> 并指定 <strong>StorPortVirtualDevice</strong> 规则。</p>
使用以下步骤来运行代码分析：
<ol>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#preparing-your-source-code" data-raw-source="[Prepare your code (use role type declarations).](./using-static-driver-verifier-to-find-defects-in-drivers.md#preparing-your-source-code)">准备你的代码 (使用) 的角色类型声明。</a></li>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#running-static-driver-verifier" data-raw-source="[Run Static Driver Verifier.](./using-static-driver-verifier-to-find-defects-in-drivers.md#running-static-driver-verifier)">运行静态驱动程序验证程序。</a></li>
<li><a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers#viewing-and-analyzing-the-results" data-raw-source="[View and analyze the results.](./using-static-driver-verifier-to-find-defects-in-drivers.md#viewing-and-analyzing-the-results)">查看并分析结果。</a></li>
</ol>
<p>有关详细信息，请参阅 <a href="/windows-hardware/drivers/devtest/using-static-driver-verifier-to-find-defects-in-drivers" data-raw-source="[Using Static Driver Verifier to Find Defects in Drivers](./using-static-driver-verifier-to-find-defects-in-drivers.md)">使用静态驱动程序验证器查找驱动程序中的缺陷</a>。</p></td>
</tr>
</tbody>
</table>

