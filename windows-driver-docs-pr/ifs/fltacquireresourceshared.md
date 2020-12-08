---
title: FltAcquireResourceShared 例程
description: FltAcquireResourceShared 例程通过调用线程获取用于共享访问的给定资源。
keywords:
- FltAcquireResourceShared 例程可安装文件系统驱动程序
topic_type:
- apiref
api_name:
- FltAcquireResourceShared
api_location:
- FltMgr.lib
- FltMgr.dll
api_type:
- LibDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 934bf430ad0ff9c31908455ec91b198baa872cb4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806303"
---
# <a name="fltacquireresourceshared-routine"></a>FltAcquireResourceShared 例程


**FltAcquireResourceShared** 例程通过调用线程获取用于共享访问的给定资源。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
VOID FltAcquireResourceShared(
  _Inout_ PERESOURCE Resource
);
```

<a name="parameters"></a>参数
----------

*资源* \[in、out\]  
指向不透明的 ERESOURCE 结构的指针。 此结构必须由调用方从非分页池分配，并通过调用 [**ExInitializeResourceLite**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializeresourcelite) 或 [**ExReinitializeResourceLite**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exreinitializeresourcelite)进行初始化。

<a name="return-value"></a>返回值
------------

无

<a name="remarks"></a>备注
-------

此例程在 Microsoft Windows XP SP2、Microsoft Windows Server 2003 SP1 及更高版本上可用。

**FltAcquireResourceShared** 例程通过调用线程获取用于共享访问的给定资源。

是否向调用方授予对给定资源的共享访问权限取决于以下各项：

-   如果资源当前为无所有者，则立即向当前线程授予共享访问权限。

-   如果调用方已获取共享或独占访问) 的资源 (，则会以递归方式授予当前线程相同的访问类型。 请注意，进行此调用不会将给定资源的调用方的独占所有权转换为 "共享"。

-   如果资源当前由另一个线程拥有，并且没有线程等待对资源的独占访问，则立即向调用方授予共享访问权限。 如果存在独占等待程序，则调用方进入等待状态。

-   如果资源当前由另一个线程拥有，或者有另一个线程正在等待独占访问，并且调用方没有资源的共享访问权限，则当前线程将进入等待状态，直到可以获取资源。

**FltAcquireResourceShared** 是用于禁用正常内核 APC 传递的 [**ExAcquireResourceSharedLite**](/previous-versions/ff544363(v=vs.85)) 的包装。

因为 **FltAcquireResourceShared** 禁用正常内核 APC 传递，所以在调用 **FltAcquireResourceShared** 之前无需调用 [**KeEnterCriticalRegion**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion)或 [**FsRtlEnterFileSystem**](fsrtlenterfilesystem.md) 。

若要在获取资源后释放资源，请调用 [**FltReleaseResource**](fltreleaseresource.md)。 必须通过对 **FltReleaseResource** 的后续调用来匹配每个对 **FltAcquireResourceShared** 的成功调用。

若要获取独占访问的资源，请调用 [**FltAcquireResourceExclusive**](fltacquireresourceexclusive.md)。

若要从系统资源列表中删除资源，请调用 [**ExDeleteResourceLite**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeleteresourcelite)。

若要初始化资源以供重用，请调用 [**ExReinitializeResourceLite**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exreinitializeresourcelite)。

有关 ERESOURCE 结构的详细信息，请参阅内核体系结构设计指南中的 [ERESOURCE 例程简介](../kernel/introduction-to-eresource-routines.md) 。

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
<td align="left"><a href="https://go.microsoft.com/fwlink/p/?linkid=531356" data-raw-source="[Universal](https://go.microsoft.com/fwlink/p/?linkid=531356)">通用</a></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Fltkernel (包含 Fltkernel) </td>
</tr>
<tr class="odd">
<td align="left"><p>库</p></td>
<td align="left">FltMgr</td>
</tr>
<tr class="even">
<td align="left"><p>IRQL</p></td>
<td align="left"><p>&lt;= APC_LEVEL</p></td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**ExAcquireResourceSharedLite**](/previous-versions/ff544363(v=vs.85))

[**ExDeleteResourceLite**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exdeleteresourcelite)

[**ExInitializeResourceLite**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exinitializeresourcelite)

[**ExReinitializeResourceLite**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exreinitializeresourcelite)

[**FltAcquireResourceExclusive**](fltacquireresourceexclusive.md)

[**FltReleaseResource**](fltreleaseresource.md)

[**FsRtlEnterFileSystem**](fsrtlenterfilesystem.md)

[**KeEnterCriticalRegion**](/windows-hardware/drivers/ddi/ntddk/nf-ntddk-keentercriticalregion)

 

