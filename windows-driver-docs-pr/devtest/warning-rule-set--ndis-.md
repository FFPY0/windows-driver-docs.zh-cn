---
title: 警告规则集 (NDIS)
description: 了解如何使用规则 (NDIS) 验证驱动程序是否可以在不同的上下文中正确处理 Irp，并遵循 Microsoft 推荐的最佳做法。
ms.date: 05/21/2018
ms.localizationpriority: medium
ms.openlocfilehash: c6d0843ad6b97c26aa7bc277a534d37a405b0164
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787571"
---
# <a name="warning-rule-set-ndis"></a>警告规则集 (NDIS)


使用这些规则来验证驱动程序是否可以在不同的上下文中正确处理 Irp，并遵循 Microsoft 推荐的最佳做法。

## <a name="in-this-section"></a>在本节中


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">主题</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="ndis-ndisstallexecution-delay.md" data-raw-source="[&lt;strong&gt;NdisStallExecution_Delay&lt;/strong&gt;](ndis-ndisstallexecution-delay.md)"><strong>NdisStallExecution_Delay</strong></a></p></td>
<td align="left"><p>NdisStallExecution_Delay 规则指定绝不能使用大于50微秒的<em>MicrosecondsToStall</em>值调用<strong>NdisStallExecution</strong> 。</p></td>
</tr>
</tbody>
</table>

 

**选择警告规则集**

1.  选择你的驱动程序项目 () 在 Microsoft Visual Studio 中。 在 " **驱动程序** " 菜单中，单击 " **启动静态驱动程序验证程序 ...**"。

2.  单击 " **规则** " 选项卡。在 " **规则集**" 下，选择 " **警告**"。

    若要从 Visual Studio 开发人员命令提示符窗口中选择默认规则集，请指定带有 **/check** 选项的 **sdv** 。 例如：

    ```
    msbuild /t:sdv /p:Inputs="/check:Warning.sdv" mydriver.VcxProj /p:Configuration="Win8 Release" /p:Platform=Win32
    ```

    有关详细信息，请参阅 [使用静态驱动程序验证器查找驱动程序中的缺陷](./using-static-driver-verifier-to-find-defects-in-drivers.md) 和 [静态驱动程序验证程序命令 (MSBuild) ](./-static-driver-verifier-commands--msbuild-.md)。

 

