---
title: FSCTL_OFFLOAD_WRITE 控制代码
description: FSCTL \_ 卸载 \_ 写入控制代码为支持卸载写入基元的存储系统中的数据块启动卸载写入。
keywords:
- FSCTL_OFFLOAD_WRITE 控制代码可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- FSCTL_OFFLOAD_WRITE
api_location:
- ntifs.h
api_type:
- HeaderDef
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd8f8be14d82624360c67b08df023b67af0bace4
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808331"
---
# <a name="fsctl_offload_write-control-code"></a>FSCTL \_ 卸载 \_ 写入控制代码


**FSCTL \_ 卸载 \_ 写入** 控制代码为支持卸载写入基元的存储系统中的数据块启动卸载写入。

要执行此操作，微筛选器驱动程序将调用 [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 与以下参数、文件系统、重定向程序和旧文件系统筛选器驱动程序调用 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) ，并提供以下参数。

**Parameters**

<a href="" id="instance--in-"></a>*实例 \[\]*  
仅 [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 调用方的不透明实例指针。 此参数是必需的，不能为 NULL。

<a href="" id="fileobject--in-"></a>*FileObject \[ in\]*  
仅 [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile) 。 文件指针对象，指定要写入的文件。 此参数是必需的，不能为 NULL。

<a href="" id="filehandle--in-"></a>*FileHandle \[\]*  
仅 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85)) 。 要写入的文件的文件句柄。 此参数是必需的，不能为 NULL。

<a href="" id="fscontrolcode--in-"></a>*FsControlCode \[\]*  
操作的控制代码。 将 **FSCTL \_ 卸载 \_ 写入** 用于此操作。

<a href="" id="inputbuffer"></a>*InputBuffer*  
指向 [**FSCTL \_ 卸载 \_ 写入 \_ 输入**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsctl_offload_write_input) 结构的指针，该结构包含要读取的数据块的大小和偏移量。

<a href="" id="inputbufferlength--in-"></a>*InputBufferLength \[\]*  
*InputBuffer* 指向的缓冲区的大小（以字节为单位）。 此值为 **sizeof** (FSCTL \_ 卸载 \_ 写入 \_ 输入输入) 。

<a href="" id="outputbuffer--out-"></a>*OutputBuffer \[\]*  
指向 [**FSCTL \_ 卸载 \_ 写入 \_ 输入**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsctl_offload_write_input) 结构的指针，该结构包含要读取的数据块的大小和偏移量。

<a href="" id="outputbufferlength--out-"></a>*OutputBufferLength \[\]*  
*OutputBuffer* 参数指向的缓冲区的大小（以字节为单位）。 此值必须至少为 **sizeof** (FSCTL \_ 卸载 \_ 读取 \_ 输出) 。

<a name="status-block"></a>状态块
------------

如果操作成功，则 [**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)或 [**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85))返回状态 \_ SUCCESS。 否则，相应的函数可能会返回以下 NTSTATUS 值之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">术语</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>STATUS_INVALID_DEVICE_REQUEST</strong></p></td>
<td align="left"><p>指定的句柄不是有效的文件句柄。</p></td>
</tr>
<tr class="even">
<td align="left"><p> <strong>STATUS_INVALID_PARAMETER</strong></p></td>
<td align="left"><p>文件大小小于 PAGE_SIZE。</p>
<p>-或-</p>
<p><em>InputBufferLength</em> &lt;<strong>sizeof</strong> (FSCTL_OFFLOAD_WRITE_INPUT) 。</p>
<p>-或-</p>
<p><a href="/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsctl_offload_write_input" data-raw-source="[&lt;strong&gt;FSCTL_OFFLOAD_WRITE_INPUT&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsctl_offload_write_input)"><strong>FSCTL_OFFLOAD_WRITE_INPUT</strong></a>中的一个或多个成员不正确：</p>
<strong>FileOffset</strong> 不是卷的逻辑扇区大小的倍数。
<strong>CopyLength</strong> 不是卷的逻辑扇区大小的倍数。
<strong>TransferOffset</strong> 不是卷的逻辑扇区大小的倍数。
<strong>大小</strong> 不是 <a href="/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsctl_offload_write_input" data-raw-source="[&lt;strong&gt;FSCTL_OFFLOAD_WRITE_INPUT&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsctl_offload_write_input)"><strong>FSCTL_OFFLOAD_WRITE_INPUT</strong></a> 结构的大小。
<strong>FileOffset</strong> &gt; 文件的有效数据长度 (VDL) 。
<strong>FileOffset</strong> + <strong>CopyLength</strong> &gt; <strong>MAXULONGLONG</strong>。</td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_NOT_SUPPORTED</strong></p></td>
<td align="left"><p>此卷上不支持卸载读取操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_OFFLOAD_WRITE_FILE_NOT_SUPPORTED</strong></p></td>
<td align="left"><p>请求的文件类型不受支持。 以下文件类型不支持卸载操作：</p>
<ul>
<li>事务性文件 (TxF) </li>
<li>非用户文件</li>
<li>压缩文件</li>
<li>稀疏文件</li>
<li>加密文件</li>
<li>NTFS 元数据文件</li>
</ul></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_TOO_LATE</strong></p></td>
<td align="left"><p>在卸载卷后尝试写入操作。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_FILE_DELETED</strong></p></td>
<td align="left"><p>此文件的数据流无效。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_FILE_CLOSED</strong></p></td>
<td align="left"><p>文件句柄已关闭。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_INVALID_HANDLE</strong></p></td>
<td align="left"><p>指定的文件句柄无效。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_FILE_LOCK_CONFLICT</strong></p></td>
<td align="left"><p>由于当前文件锁定状态，无法授予读取或写入访问权限。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_END_OF_FILE</strong></p></td>
<td align="left"><p><a href="/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsctl_offload_write_input" data-raw-source="[&lt;strong&gt;FSCTL_OFFLOAD_WRITE_INPUT&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsctl_offload_write_input)"><strong>FSCTL_OFFLOAD_WRITE_INPUT</strong></a>的<strong>FileOffset</strong>成员将在文件尾 (EOF) 开始后开始。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_DISMOUNTED_VOLUME</strong></p></td>
<td align="left"><p>卸载写入无法在卸除的卷上发生。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_MEDIA_WRITE_PROTECTED</strong></p></td>
<td align="left"><p>卷为只读。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>STATUS_INSUFFICIENT_RESOUCES</strong></p></td>
<td align="left"><p>资源不足，无法完成请求。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>STATUS_BUFFER_TOO_SMALL</strong></p></td>
<td align="left"><p><em>InputBufferLength</em> 太小， <em>InputBuffer</em> 无法包含 <a href="/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsctl_offload_write_input" data-raw-source="[&lt;strong&gt;FSCTL_OFFLOAD_WRITE_INPUT&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsctl_offload_write_input)"><strong>FSCTL_OFFLOAD_WRITE_INPUT</strong></a> 结构。</p>
<p>-或-</p>
<p><em>OutputBufferLength</em> 太小， <em>OutputBuffer</em> 无法接收 <a href="/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsctl_offload_write_output" data-raw-source="[&lt;strong&gt;FSCTL_OFFLOAD_WRITE_OUTPUT&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsctl_offload_write_output)"><strong>FSCTL_OFFLOAD_WRITE_OUTPUT</strong></a> 结构。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

卸载读取仅适用于普通文件。 有关不支持的文件类型的列表，请参阅 **\_ \_ \_ \_ 不 \_ 支持状态卸载写入文件** 的描述。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>版本</p></td>
<td align="left"><p>从 Windows 8 开始可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Ntifs (包含 Ntifs 或 Fltkernel) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**FltFsControlFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltfscontrolfile)

[**ZwFsControlFile**](/previous-versions/ff566462(v=vs.85))

[**FSCTL \_ 卸载 \_ 写入 \_ 输入**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsctl_offload_write_input)

[**FSCTL \_ 卸载 \_ 写入 \_ 输出**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_fsctl_offload_write_output)

