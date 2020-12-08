---
title: IRP_MJ_QUERY_EA 联合的 FLT_PARAMETERS
description: 当 IRP_MJ_QUERY_EA 操作的 FLT_IO_PARAMETER_BLOCK 结构的 MajorFunction 字段时使用的联合组件。
keywords:
- IRP_MJ_QUERY_EA 联合可安装文件系统驱动程序的 FLT_PARAMETERS
- FLT_PARAMETERS 联合可安装文件系统驱动程序
- PFLT_PARAMETERS 联合指针可安装的文件系统驱动程序
topic_type:
- apiref
api_name:
- FLT_PARAMETERS
api_location:
- fltkernel.h
api_type:
- HeaderDef
ms.date: 02/04/2020
ms.localizationpriority: medium
ms.openlocfilehash: 89fbcf9f25f58d61689e711d18f3f4cd85172c83
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96792911"
---
# <a name="flt_parameters-for-irp_mj_query_ea-union"></a>IRP_MJ_QUERY_EA 联合的 FLT_PARAMETERS

当 [**IRP_MJ_QUERY_EA**](irp-mj-query-ea.md)操作的 [**FLT_IO_PARAMETER_BLOCK**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)结构的 **MajorFunction** 字段时使用的联合组件。

## <a name="syntax"></a>语法

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    ULONG                    Length;
    PVOID                    EaList;
    ULONG                    EaListLength;
    ULONG  POINTER_ALIGNMENT EaIndex;
    PVOID                    EaBuffer;
    PMDL                     MdlAddress;
  } QueryEa;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

## <a name="members"></a>成员

**QueryEa**  
包含以下成员 FLT_PARAMETERS 联合内的结构。

**长度**  
**EaBuffer** 指向的缓冲区的长度（以字节为单位）。

**EaList**  
指向调用方提供的、FILE_GET_EA_INFORMATION 结构化输入缓冲区的指针，它指定要查询的扩展属性。

**EaListLength**  
**EaList** 指向的缓冲区的长度（以字节为单位）。

**EaIndex**  
开始扫描扩展属性列表的项的索引。 如果未在操作的 FLT_IO_PARAMETER_BLOCK 结构中设置 SL_INDEX_SPECIFIED 标志，或者如果 **EaList** 指向非空列表，则忽略此参数。

**EaBuffer**  
指向调用方提供的、 [**FILE_FULL_EA_INFORMATION**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_full_ea_information)结构化的输出缓冲区的指针，将在其中返回扩展特性值。 此成员是可选的，如果 **MdlAddress** 中提供 MDL，此成员可以为 **NULL** 。 请参阅 " **备注**"。

**MdlAddress**  
 (MDL 的内存描述符列表的地址) 描述 **EaBuffer** 指向的缓冲区。 此成员是可选的，如果 **EaBuffer** 中提供了缓冲区，则可以为 **NULL** 。 请参阅 " **备注**"。

## <a name="remarks"></a>备注

[**IRP_MJ_QUERY_EA**](irp-mj-query-ea.md)操作的 [**FLT_PARAMETERS**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)结构包含由回调数据表示的基于 IRP 的查询扩展属性-信息操作的参数 ([**FLT_CALLBACK_DATA**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)) 结构。 它包含在 FLT_IO_PARAMETER_BLOCK 结构中。

如果同时提供了 **EaBuffer** 和 **MdlAddress** 缓冲区，则建议 minifilters 使用 MDL。 当 **EaBuffer** 指向的内存是在调用进程的上下文中访问的用户模式地址时，或者如果它是内核模式地址，则它是有效的。

如果微筛选器更改 **MdlAddress** 的值，则在其后回拨后，筛选器管理器将释放当前存储在 **MDLADDRESS** 中的 MDL，并还原以前的 **MdlAddress** 值。

IRP_MJ_QUERY_EA 是基于 IRP 的操作。

## <a name="requirements"></a>要求

**标头**： Fltkernel (包含 Fltkernel) 


## <a name="see-also"></a>请参阅

[**FILE_FULL_EA_INFORMATION**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_full_ea_information)

[**FLT_CALLBACK_DATA**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[**FLT_IO_PARAMETER_BLOCK**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[**FLT_IS_FASTIO_OPERATION**](/windows-hardware/drivers/ddi/index)

[**FLT_IS_FS_FILTER_OPERATION**](/previous-versions/ff544648(v=vs.85))

[**FLT_IS_IRP_OPERATION**](/previous-versions/ff544654(v=vs.85))

[**FLT_PARAMETERS**](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**IoCheckEaBufferValidity**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iocheckeabuffervalidity)

[**IRP_MJ_QUERY_EA**](irp-mj-query-ea.md)
