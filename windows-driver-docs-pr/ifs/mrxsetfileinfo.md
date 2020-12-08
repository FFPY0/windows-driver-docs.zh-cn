---
title: MRxSetFileInfo 例程
description: MRxSetFileInfo 例程由 RDBSS 调用，请求网络小型重定向程序在文件系统对象上设置文件信息。
keywords:
- MRxSetFileInfo 例程可安装文件系统驱动程序
- PMRX_CALLDOWN
topic_type:
- apiref
api_name:
- MRxSetFileInfo
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 31fe0087dd918e19fc9d71710a013ea50b1964c7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831479"
---
# <a name="mrxsetfileinfo-routine"></a>MRxSetFileInfo 例程


*MRxSetFileInfo* 例程由 [RDBSS](./the-rdbss-driver-and-library.md)调用，请求网络小型重定向程序在文件系统对象上设置文件信息。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxSetFileInfo;

NTSTATUS MRxSetFileInfo(
  _Inout_ PRX_CONTEXT RxContext
)
{ ... }
```

<a name="parameters"></a>参数
----------

*RxContext* \[in、out\]  
指向 RX \_ 上下文结构的指针。 此参数包含请求操作的 IRP。

<a name="return-value"></a>返回值
------------

*MRxSetFileInfo* 返回成功的状态 \_ 成功或适当的 NTSTATUS 值，如以下之一：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">返回代码</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>STATUS_ACCESS_DENIED</strong></td>
<td align="left"><p>调用方缺乏此操作的正确安全性。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_INSUFFICIENT_RESOURCES</strong></td>
<td align="left"><p>资源不足，无法完成查询。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_INVALID_PARAMETER</strong></td>
<td align="left"><p>指定的参数无效。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_NETWORK_ACCESS_DENIED</strong></td>
<td align="left"><p>网络访问被拒绝。 如果要求网络小型重定向程序在只读共享上设置文件信息，则可能会返回此错误。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_NOT_IMPLEMENTED</strong></td>
<td align="left"><p>未实现请求的功能，如在远程页面文件上设置文件信息。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_OBJECT_NAME_NOT_FOUND</strong></td>
<td align="left"><p>找不到对象名称。 如果要求网络小型重定向程序设置文件的文件信息，但该文件不存在，则会返回此错误。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_OBJECT_PATH_NOT_FOUND</strong></td>
<td align="left"><p>找不到对象路径。 如果已传递 NTFS 流对象，而远程文件系统不支持流，则可以返回此错误。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_ONLY_IF_CONNECTED</strong></td>
<td align="left"><p>未连接 SRV_OPEN 结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_REPARSE</strong></td>
<td align="left"><p>需要重新分析才能处理符号链接。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

RDBSS 发出对 *MRxSetFileInfo* 的调用，以响应接收 [**IRP \_ MJ \_ 集 \_ 信息**](irp-mj-set-information.md) 请求。

在调用 *MRxSetFileInfo* 之前，RDBSS 会修改 \_ *RXCONTEXT* 参数指向的 RX 上下文结构中的以下成员：

**FileInformationClass** 成员设置为 **IrpSp- &gt; SetFile. FileInformationClass**，即指定的文件 \_ 信息 \_ 类值。

**Info. Buffer** 成员设置为 **Irp- &gt;AssociatedIrp.SystemBuffer**。

**信息. length** 成员设置为 IrpSp. **&gt; SetFile**。

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
<td align="left">Mrx (包含 Mrx) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**MRxIsValidDirectory**](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_chkdir_calldown)

[**MRxQueryDirectory**](mrxquerydirectory.md)

[**MRxQueryEaInfo**](mrxqueryeainfo.md)

[**MRxQueryFileInfo**](mrxqueryfileinfo.md)

[**MRxQueryQuotaInfo**](mrxqueryquotainfo.md)

[**MRxQuerySdInfo**](mrxquerysdinfo.md)

[**MRxQueryVolumeInfo**](mrxqueryvolumeinfo.md)

[**MRxSetEaInfo**](mrxseteainfo.md)

[**MRxSetFileInfoAtCleanup**](mrxsetfileinfoatcleanup.md)

[**MRxSetQuotaInfo**](mrxsetquotainfo.md)

[**MRxSetSdInfo**](mrxsetsdinfo.md)

[**MRxSetVolumeInfo**](mrxsetvolumeinfo.md)

 

