---
title: 'IRP_MJ_QUERY_INFORMATION (IFS) '
description: IRP\_MJ\_QUERY\_INFORMATION
keywords:
- IRP_MJ_QUERY_INFORMATION 可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- IRP_MJ_QUERY_INFORMATION
api_type:
- NA
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: df98c6da1db4ab65b7784bd759cb822856a54fb5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836461"
---
# <a name="irp_mj_query_information-ifs"></a>\_ \_ (IFS) 的 IRP MJ 查询 \_ 信息


## <a name="when-sent"></a>发送时间


IRP \_ MJ \_ 查询 \_ 信息请求由 i/o 管理器和其他操作系统组件以及其他内核模式驱动程序发送。 例如，在用户模式应用程序调用 Microsoft Win32 函数（如 **GetFileInformationByHandle** ）或内核模式组件已调用 [**ZwQueryInformationFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntqueryinformationfile)时，可以发送此请求。

## <a name="operation-file-system-drivers"></a>操作：文件系统驱动程序


文件系统驱动程序应提取并解码文件对象，以确定它是否表示用户打开了文件或目录。 如果是这样，则驱动程序应处理查询并完成 IRP。 否则，驱动程序应视需要完成 IRP，而不处理查询。

可以查询的文件和目录信息的类型与文件系统相关，但通常包括：

FileAllInformation FileAlternateNameInformation FileAttributeTagInformation FileBasicInformation FileCompressionInformation FileEaInformation FileInternalInformation FileNameInformation FileNetworkOpenInformation FilePositionInformation FileStandardInformation FileStreamInformation FileHardLinkInformation 尽管还可以将 FileAccessInformation、FileAlignmentInformation 和 FileModeInformation 信息类型作为参数传递给 [**ZwQueryInformationFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntqueryinformationfile)，但此信息与文件系统无关。 因此， **ZwQueryInformationFile** 直接提供此信息，而无需将 IRP \_ MJ \_ 查询 \_ 信息请求发送到文件系统。

有关这些信息类型的详细信息，请参阅下面的链接。 有关所有可能的信息类型的列表，请参阅 \_ ntifs 中的文件信息 \_ 类枚举。

## <a name="operation-network-redirector-drivers"></a>操作：网络重定向程序驱动程序


网络重定向程序驱动程序不是基于 [RDBSS](./the-rdbss-driver-and-library.md) 的，接收到 \_ \_ FILEALLINFORMATION 或 FileNameInformation 的 IRP MJ 查询 \_ 信息请求，必须使用 \\ \\ \\ 单个前导反斜杠在服务器名称前使用单个前导反斜杠来响应该文件名的完整 "服务器共享文件" 路径。 对于作为通用命名约定访问的文件，必须返回此格式的名称信息 (UNC) 名称 (*\\ \\ server \\ share \\ 文件夹 \\filename.txt*，例如) 或位于映射驱动器 (*x： \\ 文件夹 \\filename.txt* 上的文件，例如) 。

对于网络微重定向程序驱动程序 (使用 rdbss.sys 动态链接的驱动程序，或者使用 rdbsslib) 进行静态链接，将 \_ \_ \_ 在 RDBSS 内部处理针对 FileNameInformation 的 IRP MJ 查询信息请求，并返回正确的名称信息。 对于网络最小化重定向程序驱动程序，FileAllInformation 的 IRP \_ MJ \_ 查询 \_ 信息请求由 RDBSS 为请求的名称信息部分在内部进行处理。 FileAllInformation 请求的其他部分作为单独的请求发送到网络微型重定向程序驱动程序以进行解析。

接收到 FileAlternateNameInformation 的 IRP MJ 查询信息请求的网络重定向程序 \_ \_ \_ 应使用不包含任何路径信息的文件的短名称 (8.3 字符) ，如果该文件存在短名称。

## <a name="operation-file-system-filter-drivers"></a>操作：文件系统筛选器驱动程序


筛选器驱动程序应将此 IRP 传递到堆栈上的下一个较低的驱动程序。

## <a name="parameters"></a>参数


文件系统或筛选器驱动程序与给定的 IRP 一起调用 [**IoGetCurrentIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation) ，以获取指向其自己的 *IrpSp*[**堆栈位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)的指针，如以下列表所示。  (IRP 显示为 *irp*。 ) 驱动程序可以使用在处理查询文件信息请求中的以下 irp 成员和 irp 堆栈位置设置的信息：

<a href="" id="deviceobject"></a>*DeviceObject*  
指向目标设备对象的指针。

<a href="" id="irp--associatedirp-systembuffer"></a>*Irp- &gt;AssociatedIrp.SystemBuffer*  
一个指针，指向要返回文件或目录信息的输出缓冲区。 此信息存储在以下结构之一中：

\_全部文件 \_

文件 \_ 属性 \_ 标记 \_ 信息

文件 \_ 基本 \_ 信息

文件 \_ 压缩 \_ 信息

文件 \_ EA \_ 信息

文件 \_ 内部 \_ 信息

文件名 \_ \_ 信息

文件 \_ 网络 \_ 打开 \_ 信息

文件 \_ 位置 \_ 信息

文件 \_ 标准 \_ 信息

文件 \_ 流 \_ 信息

文件 \_ 链接 \_ 信息

<a href="" id="irp--iostatus"></a>*Irp- &gt;IoStatus* 指向 [**IO \_ 状态 \_ 块**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block) 结构的指针，该结构接收最终完成状态和有关请求的操作的信息。 有关详细信息，请参阅 [**ZwQueryInformationFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntqueryinformationfile)中的 *IoStatusBlock* 参数说明。 例程.

<a href="" id="irp--userbuffer"></a>*Irp- &gt;UserBuffer* 可选指针，指向调用方提供的输出缓冲区，在 i/o 管理器的 i/o 完成过程中，会将 *Irp &gt;AssociatedIrp.SystemBuffer* 的内容复制到其中。 驱动程序不使用此缓冲区返回请求的任何数据。

<a href="" id="irpsp--fileobject"></a>*IrpSp- &gt;* 指向与 *DeviceObject* 关联的文件对象的 FileObject 指针。

*IrpSp- &gt; FileObject* 参数包含指向 **RelatedFileObject** 字段的指针，该字段也是文件 \_ 对象结构。 文件对象结构的 **RelatedFileObject** 字段在 \_ 处理 IRP \_ MJ 查询信息期间无效 \_ \_ ，不应使用。

<a href="" id="irpsp--majorfunction"></a>*IrpSp- &gt;MajorFunction* 指定 IRP \_ MJ \_ 查询 \_ 信息。

<a href="" id="irpsp--parameters-queryfile-fileinformationclass"></a>*IrpSp- &gt;* 要查询的文件信息的 QueryFile. FileInformationClass 类型。 此成员可以是以下值之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">“值”</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>FileAllInformation</strong></p></td>
<td align="left"><p>返回文件的 FILE_ALL_INFORMATION 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileAttributeTagInformation</strong></p></td>
<td align="left"><p>返回文件的 <a href="/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_attribute_tag_information" data-raw-source="[&lt;strong&gt;FILE_ATTRIBUTE_TAG_INFORMATION&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_attribute_tag_information)"><strong>FILE_ATTRIBUTE_TAG_INFORMATION</strong></a> 结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileBasicInformation</strong></p></td>
<td align="left"><p>返回文件的 <a href="/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_basic_information" data-raw-source="[&lt;strong&gt;FILE_BASIC_INFORMATION&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_basic_information)"><strong>FILE_BASIC_INFORMATION</strong></a> 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileCompressionInformation</strong></p></td>
<td align="left"><p>返回文件的 FILE_COMPRESSION_INFORMATION 结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileEaInformation</strong></p></td>
<td align="left"><p>返回文件的 FILE_EA_INFORMATION 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileInternalInformation</strong></p></td>
<td align="left"><p>返回文件的 <a href="/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_internal_information" data-raw-source="[&lt;strong&gt;FILE_INTERNAL_INFORMATION&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_internal_information)"><strong>FILE_INTERNAL_INFORMATION</strong></a> 结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileNameInformation</strong></p></td>
<td align="left"><p>返回文件的 <a href="/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_name_information" data-raw-source="[&lt;strong&gt;FILE_NAME_INFORMATION&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_name_information)"><strong>FILE_NAME_INFORMATION</strong></a> 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileNetworkOpenInformation</strong></p></td>
<td align="left"><p>返回文件的单个 <a href="/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_network_open_information" data-raw-source="[&lt;strong&gt;FILE_NETWORK_OPEN_INFORMATION&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_network_open_information)"><strong>FILE_NETWORK_OPEN_INFORMATION</strong></a> 结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FilePositionInformation</strong></p></td>
<td align="left"><p>返回文件的单个 <a href="/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_position_information" data-raw-source="[&lt;strong&gt;FILE_POSITION_INFORMATION&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_position_information)"><strong>FILE_POSITION_INFORMATION</strong></a> 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileStandardInformation</strong></p></td>
<td align="left"><p>返回文件的单个 <a href="/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_standard_information" data-raw-source="[&lt;strong&gt;FILE_STANDARD_INFORMATION&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_standard_information)"><strong>FILE_STANDARD_INFORMATION</strong></a> 结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>FileStreamInformation</strong></p></td>
<td align="left"><p>返回文件的单个 <a href="/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_stream_information" data-raw-source="[&lt;strong&gt;FILE_STREAM_INFORMATION&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_stream_information)"><strong>FILE_STREAM_INFORMATION</strong></a> 结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>FileHardLinkInformation</strong></p></td>
<td align="left"><p>返回文件的 <a href="/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_links_information" data-raw-source="[&lt;strong&gt;FILE_LINKS_INFORMATION&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_links_information)"><strong>FILE_LINKS_INFORMATION</strong></a> 结构。</p></td>
</tr>
</tbody>
</table>

 

<a href="" id="irpsp--parameters-queryfile-length"></a>*IrpSp- &gt;QueryFile* *&gt; temBuffer 所AssociatedIrp.Sys* 指向的缓冲区的长度（以字节为单位）。

<a name="remarks"></a>备注
-------

IRP \_ MJ \_ 查询 \_ 信息操作始终由 i/o 管理器进行缓冲。 用于返回所请求的文件或目录信息的 *Irp &gt;AssociatedIrp.SystemBuffer* 由 i/o 管理器从非分页池内存进行分配。 因此，操作系统返回的 *Irp &gt;AssociatedIrp.SystemBuffer* 将始终是 *IrpSp- &gt; QueryFile* 中指定的长度的有效地址。

*Irp- &gt; AssociatedIrp. UserBuffer* 由 i/o 管理器在内部使用，不应由文件系统或文件系统筛选器驱动程序使用。

## <a name="see-also"></a>请参阅


[**文件 \_ 对齐 \_ 信息**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_alignment_information)

[**文件 \_ 属性 \_ 标记 \_ 信息**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_attribute_tag_information)

[**文件 \_ 基本 \_ 信息**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_basic_information)

[**文件 \_ 内部 \_ 信息**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_internal_information)

[**文件名 \_ \_ 信息**](/windows-hardware/drivers/ddi/ntddk/ns-ntddk-_file_name_information)

[**文件 \_ 网络 \_ 打开 \_ 信息**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_network_open_information)

[**文件 \_ 位置 \_ 信息**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_position_information)

[**文件 \_ 标准 \_ 信息**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_standard_information)

[**文件 \_ 流 \_ 信息**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_stream_information)

[**文件 \_ 链接 \_ 信息**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_file_links_information)

[**IO \_ 堆栈 \_ 位置**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_stack_location)

[**IO \_ 状态 \_ 块**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_status_block)

[**IoCheckEaBufferValidity**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocheckeabuffervalidity)

[**IoGetCurrentIrpStackLocation**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetcurrentirpstacklocation)

[**IRP**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_irp)

[**IRP \_ MJ \_ 设置 \_ 信息**](irp-mj-set-information.md)

[**ZwQueryInformationFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntqueryinformationfile)

