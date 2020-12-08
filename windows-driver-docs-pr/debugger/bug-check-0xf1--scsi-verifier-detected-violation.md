---
title: Bug 检查 0xF1 SCSI_VERIFIER_DETECTED_VIOLATION
description: SCSI_VERIFIER_DETECTED_VIOLATION bug 检查的值为0x000000F1。 这是所有驱动程序验证器 SCSI 验证冲突的 bug 检查代码。
keywords:
- Bug 检查 0xF1 SCSI_VERIFIER_DETECTED_VIOLATION
- SCSI_VERIFIER_DETECTED_VIOLATION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- SCSI_VERIFIER_DETECTED_VIOLATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3900448910b3b1d1abc857c22a535221397b4a84
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96828267"
---
# <a name="bug-check-0xf1-scsi_verifier_detected_violation"></a>Bug 检查0xF1： SCSI \_ 验证程序 \_ 检测到 \_ 冲突


SCSI \_ 验证器 \_ 检测到 \_ 违反 bug 检查的值为0x000000F1。 这是所有驱动程序验证器 **SCSI 验证** 冲突的 bug 检查代码。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="scsi_verifier_detected_violation-parameters"></a>SCSI \_ 验证器 \_ 检测到 \_ 冲突参数


参数1标识冲突类型。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数 1</th>
<th align="left">参数2</th>
<th align="left">参数3</th>
<th align="left">参数4</th>
<th align="left">错误的原因</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x1000</p></td>
<td align="left"><p>传递的第一个参数</p></td>
<td align="left"><p>传递的第二个参数</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>微型端口驱动程序向 <strong>ScsiPortInitialize</strong>传递了错误的参数。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1001</p></td>
<td align="left"><p>延迟（微秒）</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>小型小型驱动程序名为 <strong>ScsiPortStallExecution</strong> ，指定延迟大于0.1 秒，停止处理器太长。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1002</p></td>
<td align="left"><p>耗时太长的例程的地址</p></td>
<td align="left"><p>微型端口的 HW_DEVICE_EXTENSION 地址</p></td>
<td align="left"><p>例程的持续时间（微秒）</p></td>
<td align="left"><p>端口驱动程序调用的微型端口例程所需的时间超过0.5 秒。</p>
<p> (0.5 秒是大多数例程的限制。 但是， <strong>HwInitialize</strong> 例程为5秒， <strong>FindAdapter</strong> 例程为豁免。 ) </p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1003</p></td>
<td align="left"><p>微型端口的 HW_DEVICE_EXTENSION 地址</p></td>
<td align="left"><p>SRB 的地址</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>微型端口驱动程序多次完成了一个请求。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1004</p></td>
<td align="left"><p>SRB 的地址</p></td>
<td align="left"><p>微型端口的 HW_DEVICE_EXTENSION 地址</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>微型端口驱动程序已完成具有无效 SRB 状态的请求。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1005</p></td>
<td align="left"><p>微型端口的 HW_DEVICE_EXTENSION 地址</p></td>
<td align="left"><p>LOGICAL_UNIT_EXTENSION 的地址</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>小型端口驱动程序调用 <strong>ScsiPortNotification</strong> 来请求 <strong>NextLuRequest</strong>，但未标记的请求仍处于活动状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x1006</p></td>
<td align="left"><p>微型端口的 HW_DEVICE_EXTENSION 地址</p></td>
<td align="left"><p>虚拟地址无效</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>微型端口驱动程序向 <strong>ScsiPortGetPhysicalAddress</strong>传递了无效的虚拟地址。</p>
<p> (这通常意味着提供的地址不会映射到通用缓冲区区域。 ) </p></td>
</tr>
<tr class="even">
<td align="left"><p>0x1007</p></td>
<td align="left"><p>ADAPTER_EXTENSION 的地址</p></td>
<td align="left"><p>微型端口的 HW_DEVICE_EXTENSION 地址</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>总线的重置保持期结束，但微型端口驱动程序仍有未处理的请求。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x2001</p></td>
<td align="left"><p>延迟（微秒）</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>Storport 微型端口驱动程序名为 <strong><a href="/windows-hardware/drivers/ddi/storport/nf-storport-storportstallexecution" data-raw-source="[StorPortStallExecution](/windows-hardware/drivers/ddi/storport/nf-storport-storportstallexecution)">StorPortStallExecution</a></strong> ，指定延迟时间超过0.1 秒，停止处理器的时间太长。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2002</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>不是从微型端口驱动程序的<strong><a href="/windows-hardware/drivers/ddi/storport/nc-storport-hw_find_adapter" data-raw-source="[HwStorFindAdapter](/windows-hardware/drivers/ddi/storport/nc-storport-hw_find_adapter)">HwStorFindAdapter</a></strong>例程调用<strong><a href="/windows-hardware/drivers/ddi/storport/nf-storport-storportgetuncachedextension" data-raw-source="[StorPortGetUncachedExtension](/windows-hardware/drivers/ddi/storport/nf-storport-storportgetuncachedextension)">StorPortGetUncachedExtension</a></strong> 。 <strong>StorPortGetUncachedExtension</strong>例程只能从微型端口驱动程序的<strong>HwStorFindAdapter</strong>例程中调用，且仅可用于总线主机适配器。 在调用<strong>StorPortGetUncachedExtension</strong>之前，storport 微型端口驱动程序必须将<strong><a href="/windows-hardware/drivers/ddi/storport/ns-storport-_hw_initialization_data-r1" data-raw-source="[HW_INITIALIZATION_DATA](/windows-hardware/drivers/ddi/storport/ns-storport-_hw_initialization_data-r1)">HW_INITIALIZATION_DATA</a></strong>的<strong>SrbExtensionSize</strong>设置 (Storport) 结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x2003</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>传递到 <strong><a href="/windows-hardware/drivers/ddi/storport/nf-storport-storportgetdevicebase" data-raw-source="[StorPortGetDeviceBase](/windows-hardware/drivers/ddi/storport/nf-storport-storportgetdevicebase)">StorPortGetDeviceBase</a></strong> 例程的地址无效。 <strong>StorPortGetDeviceBase</strong>例程仅支持由 system 即插即用 (PnP) manager 分配给驱动程序的地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x2004</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>Storport 微型端口驱动程序多次完成了同一 i/o 请求。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x2005</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>预留</p></td>
<td align="left"><p>Storport 微型端口驱动程序将无效的虚拟地址传递给 <strong>StorPortRead</strong><em>xxx</em> 或 <strong>StorPortWrite</strong><em>xxx</em> 例程之一。 这通常意味着提供的地址不会映射到通用缓冲区区。 指定的 <em>寄存器</em> 或 <em>端口</em> 必须在 <strong><a href="/windows-hardware/drivers/ddi/storport/nf-storport-storportgetdevicebase" data-raw-source="[StorPortGetDeviceBase](/windows-hardware/drivers/ddi/storport/nf-storport-storportgetdevicebase)">StorPortGetDeviceBase</a></strong> 例程返回的映射的内存空间范围内。</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

有关原因的说明，请参阅参数部分中每个代码的说明。

<a name="resolution"></a>解决方法
----------

此 bug 检查只能在已指示驱动程序验证器监视一个或多个驱动程序时出现。 如果你不打算使用驱动程序验证程序，则应停用它。 你可以考虑删除导致此问题的驱动程序。

如果您是驱动程序编写者，请使用通过此 bug 检查获取的信息来修复代码中的 bug。

"驱动程序验证程序" **SCSI 验证** 选项仅在 Windows XP 和更高版本中可用。 Driver Verifier **Storport 验证** 选项仅适用于 Windows 7 及更高版本。 有关驱动程序验证程序的完整详细信息，请参阅 Windows 驱动程序工具包。

