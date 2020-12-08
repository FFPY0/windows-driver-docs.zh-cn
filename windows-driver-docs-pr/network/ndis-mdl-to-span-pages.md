---
title: NDIS_MDL_TO_SPAN_PAGES 宏
description: NDIS_MDL_TO_SPAN_PAGES 宏检索正在用来返回给定 MDL 的内存物理页数。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 NDIS_MDL_TO_SPAN_PAGES 宏网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 736987011d6d61b8c47c86cf6db0637a5579f979
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96801631"
---
# <a name="ndis_mdl_to_span_pages-macro"></a>\_ \_ 用于跨页面的 NDIS MDL \_ \_ 宏


" **NDIS \_ MDL \_ 到 \_ 跨 \_ 页** " 宏检索正在用来返回给定 MDL 的内存物理页数。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
int NDIS_MDL_TO_SPAN_PAGES(
   PMDL _Mdl
);
```

<a name="parameters"></a>参数
----------

*\_Mdl*   
指向 MDL 的指针。

<a name="return-value"></a>返回值
------------

**NDIS \_MDL \_ 到 \_ 跨 \_ 页** 返回支持 MDL 虚拟范围的页数。

<a name="remarks"></a>备注
-------

" **Ndis \_ MDL \_ 到 \_ 跨 \_ 页** " 宏提供了基于 MDL 的 [**ndis 缓冲区版本 \_ \_ 来 \_ 跨 \_ 页面**](/previous-versions/windows/hardware/network/ff556922(v=vs.85)) 功能。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>目标平台</p></td>
<td>台式机</td>
</tr>
<tr class="even">
<td><p>版本</p></td>
<td><p>在 NDIS 6.0 和更高版本中受支持。</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td> (包含 Ndis .h) </td>
</tr>
<tr class="even">
<td><p>IRQL</p></td>
<td><p>任何级别</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**\_ \_ 用于 \_ 跨页的 \_ NDIS 缓冲区**](/previous-versions/windows/hardware/network/ff556922(v=vs.85))

 

