---
title: DeinterlaceQueryAvailableModes 方法
description: 示例 DXVA \_ DeinterlaceContainerDeviceClass：:D einterlacequeryavailablemodes 函数查询特定输入视频格式的可用取消隔行扫描或帧速率转换模式。
keywords:
- DeinterlaceQueryAvailableModes 方法显示设备
- DeinterlaceQueryAvailableModes 方法显示设备，DXVA_DeinterlaceContainerDeviceClass 接口
- DXVA_DeinterlaceContainerDeviceClass 接口显示设备，DeinterlaceQueryAvailableModes 方法
topic_type:
- apiref
api_name:
- DXVA_DeinterlaceContainerDeviceClass.DeinterlaceQueryAvailableModes
api_type:
- COM
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: 1e7d235bb2c25d87314d61db394032f5a53c8cd2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799741"
---
# <a name="dxva_deinterlacecontainerdeviceclassdeinterlacequeryavailablemodes-method"></a>DXVA \_ DeinterlaceContainerDeviceClass：:D einterlacequeryavailablemodes 方法


示例 *DeinterlaceQueryAvailableModes* 函数查询特定输入视频格式的可用取消隔行扫描或帧速率转换模式。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
HRESULT DeinterlaceQueryAvailableModes(
  [in]      LPDXVA_VideoDesc lpVideoDescription,
  [in, out] LPDWORD          lpdwNumModesSupported,
  [in, out] LPGUID           pGuidsDeinterlaceModes
);
```

<a name="parameters"></a>参数
----------

*lpVideoDescription* \[在中， \] 提供指向 [**DXVA \_ VideoDesc**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videodesc) 结构的指针，该结构包含要执行的取消隔行扫描或帧速率转换的视频流的说明。

*lpdwNumModesSupported* \[在中，out \] 接收到在 *pGuidsDeinterlaceModes* 的数组中返回的隔行扫描或帧速率转换模式的指针。

*pGuidsDeinterlaceModes* \[在中，out \] 接收指向 guid 数组的指针，该数组表示驱动程序支持的隔行扫描或帧速率转换模式。

<a name="return-value"></a>返回值
------------

如果成功，则返回零 (S \_ 正常或 DD \_ 确定) ; 否则返回错误代码。 有关错误代码的完整列表，请参阅 *ddraw。*

<a name="remarks"></a>备注
-------

将 *lpVideoDescription* 参数传递给驱动程序，以便驱动程序可以支持源视频的分辨率和格式。 例如，驱动程序可能能够对480i 的内容执行三字段自适应隔行扫描，但它可能只允许 bob 1080i 内容。 有关详细信息，请参阅 [用于取消隔行扫描和 Frame-Rate 转换的视频内容](./video-content-for-deinterlace-and-frame-rate-conversion.md)。

*PGuidsDeinterlaceModes* 参数返回的 guid 应按照 (的降序顺序返回，即，最高质量模式应占用) 返回的 GUID 数组的第一个元素。

所有驱动程序都应该能够使用现有的 *位块传输* (blt) 硬件支持 bob 模式。 有关模式的详细信息，请参阅 [隔行扫描模式](./deinterlace-modes.md) 和 [帧速率转换模式](./frame-rate-conversion-modes.md) 主题。

驱动程序将 (模式返回 Guid，以响应 *VMR* 的请求) 。 驱动程序将响应其 [*DdMoCompRender*](/windows/win32/api/ddrawint/nc-ddrawint-pdd_mocompcb_render) 回调函数的调用。 驱动程序通过 [**DD \_ RENDERMOCOMPDATA**](/windows/win32/api/ddrawint/ns-ddrawint-dd_rendermocompdata)结构的 **lpOutputData** 成员返回 Guid， *DdMoCompRender* 指向的 *lpRenderData* 参数。 **LpOutputData** 成员指向 [**DXVA \_ DeinterlaceQueryAvailableModes**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacequeryavailablemodes)结构，该结构包含 **guid** 成员中的 guid 数组。

**将 RenderMoComp 映射到**  **_DeinterlaceQueryAvailableModes_* _

_DeinterlaceQueryAvailableModes * 函数的示例直接映射到 [**DD \_ MOTIONCOMPCALLBACKS**](/windows/win32/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)结构的 **RenderMoComp** 成员的调用。 **RenderMoComp** 成员指向显示驱动程序提供的、引用 [**DD \_ RENDERMOCOMPDATA**](/windows/win32/api/ddrawint/ns-ddrawint-dd_rendermocompdata)结构的函数。

在未首先调用显示驱动程序提供的 **BeginMoCompFrame** 或 **EndMoCompFrame** 函数的情况下调用 **RenderMoComp** 回调。

\_按如下所示填充 DD RENDERMOCOMPDATA 结构。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">成员</th>
<th align="left">“值”</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>dwNumBuffers</strong></p></td>
<td align="left"><p>Zero。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>lpBufferInfo</strong></p></td>
<td align="left"><p>NULL。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>dwFunction</strong></p></td>
<td align="left"><p><em>DXVA</em>) 中定义<strong>DXVA_DeinterlaceQueryAvailableModesFnCode</strong>常量 (。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>lpInputData</strong></p></td>
<td align="left"><p>指向已填充 <a href="/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videodesc" data-raw-source="[&lt;strong&gt;DXVA_VideoDesc&lt;/strong&gt;](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videodesc)"><strong>DXVA_VideoDesc</strong></a> 结构的指针。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>lpOutputData</strong></p></td>
<td align="left"><p>指向 <a href="/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacequeryavailablemodes" data-raw-source="[&lt;strong&gt;DXVA_DeinterlaceQueryAvailableModes&lt;/strong&gt;](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_deinterlacequeryavailablemodes)"><strong>DXVA_DeinterlaceQueryAvailableModes</strong></a> 结构的指针。</p></td>
</tr>
</tbody>
</table>

 

在 *VMR* 确定了可用于特定视频格式的隔行扫描或帧转换模式后，VMR 将查询该驱动程序，以获取有关特定隔行扫描模式的输入要求以及该模式可能支持的任何其他视频处理的详细信息。 驱动程序将此信息从对其 [**DeinterlaceQueryModeCaps**](dxva-deinterlacecontainerdeviceclass-deinterlacequerymodecaps.md) 函数的调用返回。

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**DD \_ MOTIONCOMPCALLBACKS**](/windows/win32/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)

[**DD \_ RENDERMOCOMPDATA**](/windows/win32/api/ddrawint/ns-ddrawint-dd_rendermocompdata)

[**DeinterlaceQueryModeCaps**](dxva-deinterlacecontainerdeviceclass-deinterlacequerymodecaps.md)

[**DXVA \_ VideoDesc**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videodesc)

[**DXVA \_ SampleFormat**](/windows-hardware/drivers/ddi/dxva/ne-dxva-_dxva_sampleformat)

