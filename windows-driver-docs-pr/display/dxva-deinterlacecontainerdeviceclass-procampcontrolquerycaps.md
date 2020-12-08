---
title: ProcAmpControlQueryCaps 方法
description: 示例 DXVA \_ DeinterlaceContainerDeviceClass：:P rocampcontrolquerycaps 函数允许 VMR 查询驱动程序，以确定 ProcAmp 控制设备的输入要求以及可能支持的其他视频处理操作。
keywords:
- ProcAmpControlQueryCaps 方法显示设备
- ProcAmpControlQueryCaps 方法显示设备，DXVA_DeinterlaceContainerDeviceClass 接口
- DXVA_DeinterlaceContainerDeviceClass 接口显示设备，ProcAmpControlQueryCaps 方法
topic_type:
- apiref
api_name:
- DXVA_DeinterlaceContainerDeviceClass.ProcAmpControlQueryCaps
api_location:
- N/A
api_type:
- COM
ms.date: 12/06/2018
ms.localizationpriority: medium
ms.custom: seodec18
ms.openlocfilehash: d6469156a6736dd0266179288c425b4eee7fdf1f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96799735"
---
# <a name="dxva_deinterlacecontainerdeviceclassprocampcontrolquerycaps-method"></a>DXVA \_ DeinterlaceContainerDeviceClass：:P rocampcontrolquerycaps 方法


示例 *ProcAmpControlQueryCaps* 函数允许 *VMR* 查询驱动程序，以确定 ProcAmp 控制设备的输入要求以及可能支持的其他视频处理操作。 查询可以在执行 ProcAmp 调整操作的同时进行。

<a name="syntax"></a>语法
------

```cpp
HRESULT ProcAmpControlQueryCaps(
  [in]  DXVA_VideoDesc          *lpVideoDescription,
  [out] DXVA_ProcAmpControlCaps *lpProcAmpCaps
);
```

<a name="parameters"></a>参数
----------

*lpVideoDescription* \[在中， \] 提供指向 [**DXVA \_ VideoDesc**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videodesc) 结构的指针，该结构定义要处理的视频的 ProcAmp 控制参数。

*lpProcAmpCaps* \[out \] 接收指向 [**DXVA \_ ProcAmpControlCaps**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_procampcontrolcaps) 结构的指针，该结构包含 ProcAmp 控件操作的驱动程序功能。

<a name="return-value"></a>返回值
------------

如果成功，则返回零 (S \_ 正常或 DD \_ 确定) ; 否则返回错误代码。 有关错误代码的完整列表，请参阅 *ddraw。*

<a name="remarks"></a>备注
-------

驱动程序将其功能报告给 ProcAmp 控件模式的用户模式组件，该组件位于 *lpProcAmpCaps* 指向的 [**DXVA \_ ProcAmpControlCaps**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_procampcontrolcaps)结构中。

示例 *ProcAmpControlQueryCaps* 函数直接映射到 [**DD \_ MOTIONCOMPCALLBACKS**](/windows/win32/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)结构的 **RenderMoComp** 成员的调用。 **RenderMoComp** 函数指向驱动程序提供的 *DdMoCompRender* 回调，该回调引用 [**DD \_ RENDERMOCOMPDATA**](/windows/win32/api/ddrawint/ns-ddrawint-dd_rendermocompdata)结构。 \_按如下所示填充 DD RENDERMOCOMPDATA 结构。

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
<td align="left"><p>零</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>lpBufferInfo</strong></p></td>
<td align="left"><p>Null</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>dwFunction</strong></p></td>
<td align="left"><p><strong>DXVA_ProcAmpControlQueryCapsFnCode</strong> 在 <em>DXVA</em> 中定义的常量 () </p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>lpInputData</strong></p></td>
<td align="left"><p>指向已填充 <a href="/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videodesc" data-raw-source="[&lt;strong&gt;DXVA_VideoDesc&lt;/strong&gt;](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videodesc)"><strong>DXVA_VideoDesc</strong></a> 结构的指针。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>lpOutputData</strong></p></td>
<td align="left"><p>指向 <a href="/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_procampcontrolcaps" data-raw-source="[&lt;strong&gt;DXVA_ProcAmpControlCaps&lt;/strong&gt;](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_procampcontrolcaps)"><strong>DXVA_ProcAmpControlCaps</strong></a> 结构的指针。</p></td>
</tr>
</tbody>
</table>

 

请注意，在未首先调用显示驱动程序提供的 BeginMoCompFrame 或 EndMoCompFrame 函数的情况下，将调用 RenderMoComp 函数。

**示例代码**

下面的代码提供了一个示例，说明如何实现 *ProcAmpControlQueryCaps* 函数：

```cpp
HRESULT
DXVA_DeinterlaceContainerDeviceClass::ProcAmpControlQueryCaps(
    LPDXVA_VideoDesc lpVideoDesc,
    LPDXVA_ProcAmpControlCaps lpProcAmpControlCaps
    )
{
    // only the YUY2 and YV12 formats can be operated on
    if (lpVideoDesc->d3dFormat != '2YUY' &&
        lpVideoDesc->d3dFormat != '21VY') {
        return E_INVALIDARG;
    }
    lpProcAmpControlCaps->InputPool = D3DPOOL_DEFAULT;
    lpProcAmpControlCaps->d3dOutputFormat = lpVideoDesc->d3dFormat;
    lpProcAmpControlCaps->ProcAmpControlProps =
        DXVA_ProcAmp_Brightness |
        DXVA_ProcAmp_Contrast |
        DXVA_ProcAmp_Hue |
        DXVA_ProcAmp_Saturation;
    lpProcAmpControlCaps->VideoProcessingCaps = DXVA_VideoProcess_None;
    return S_OK;
}
```

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>目标平台</p></td>
<td align="left">台式机</td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">在驱动程序提供的标头文件中声明了不 () 。</td>
</tr>
</tbody>
</table>

## <a name="span-idsee_alsospansee-also"></a><span id="see_also"></span>另请参阅


[**DXVA \_ VideoDesc**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_videodesc)

[**DXVA \_ ProcAmpControlCaps**](/windows-hardware/drivers/ddi/dxva/ns-dxva-_dxva_procampcontrolcaps)

[**DD \_ MOTIONCOMPCALLBACKS**](/windows/win32/api/ddrawint/ns-ddrawint-dd_motioncompcallbacks)

[**DD \_ RENDERMOCOMPDATA**](/windows/win32/api/ddrawint/ns-ddrawint-dd_rendermocompdata)

