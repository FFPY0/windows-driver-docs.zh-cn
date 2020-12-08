---
title: IRP_MJ_CREATE 联合的 FLT_PARAMETERS
description: 当 IRP_MJ_CREATE 操作的 FLT_IO_PARAMETER_BLOCK 结构的 MajorFunction 字段时，将使用以下联合组件。
keywords:
- IRP_MJ_CREATE 联合可安装文件系统驱动程序的 FLT_PARAMETERS
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
ms.date: 11/05/2019
ms.localizationpriority: medium
ms.openlocfilehash: a86137a97d248c68fc7a4949734b47d6a1546b8f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96803563"
---
# <a name="flt_parameters-for-irp_mj_create-union"></a>IRP_MJ_CREATE 联合的 FLT_PARAMETERS

当 [**IRP_MJ_CREATE**](irp-mj-create.md)操作的 [FLT_IO_PARAMETER_BLOCK](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)结构的 **MajorFunction** 字段时，将使用以下联合组件。

## <a name="syntax"></a>语法

```ManagedCPlusPlus
typedef union _FLT_PARAMETERS {
  ...    ;
  struct {
    PIO_SECURITY_CONTEXT     SecurityContext;
    ULONG                    Options;
    USHORT POINTER_ALIGNMENT FileAttributes;
    USHORT                   ShareAccess;
    USHORT POINTER_ALIGNMENT EaLength;
    PVOID                    EaBuffer;
    LARGE_INTEGER            AllocationSize;
  } Create;
  ...    ;
} FLT_PARAMETERS, *PFLT_PARAMETERS;
```

## <a name="members"></a>成员

FLT_PARAMETERS 的 **Create** 结构包含以下成员。

**SecurityContext**

一个指向 [IO_SECURITY_CONTEXT](/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_io_security_context) 结构的指针，该结构表示 IRP_MJ_CREATE 请求的安全上下文，其中：

- **SecurityContext->AccessState** 是一个指向 [ACCESS_STATE](/windows-hardware/drivers/ddi/wdm/ns-wdm-_access_state) 结构的指针，该结构包含对象的主题上下文、授予访问类型和剩余所需的访问类型。

- **SecurityContext->DesiredAccess** 是一个 [ACCESS_MASK](../kernel/access-mask.md) 结构，它指定为文件请求的访问权限。 有关详细信息，请参阅 [**FltCreateFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatefile)的 *DesiredAccess* 参数。

**选项**  
标志的位掩码，用于指定创建或打开该文件时要应用的选项，以及在文件已存在时要执行的操作。 此成员的低24位对应于 [**FltCreateFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatefile)的 *CreateOptions* 参数。 高8位对应于 **FltCreateFile** 的 *CreateDisposition* 参数。

**FileAttributes**  
创建或打开文件时要应用的属性的位掩码。 有关详细信息，请参阅 [**FltCreateFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatefile)的 *FileAttributes* 参数。

**ShareAccess**  
为文件请求的共享访问权限位掩码。 如果此参数为零，则请求独占访问。 有关详细信息，请参阅 [**FltCreateFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatefile)的 *ShareAccess* 参数。

**EaLength**  
**EaBuffer** 成员指向的缓冲区的长度（以字节为单位）。 有关详细信息，请参阅 [**FltCreateFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatefile)的 *EaLength* 参数。

**EaBuffer**  
一个指向调用方提供的 [FILE_FULL_EA_INFORMATION](/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_full_ea_information)结构化缓冲区的指针，该缓冲区包含要应用于该文件 (EA) 信息的扩展属性。 有关详细信息，请参阅 [**FltCreateFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatefile)的 *EaBuffer* 参数。

**AllocationSize**  
（可选）指定文件的初始分配大小（以字节为单位）。 如果创建、覆盖或取代了文件，则非零值将不起作用。 有关详细信息，请参阅 [**FltCreateFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatefile)的 *AllocationSize* 参数。

## <a name="remarks"></a>备注

[IRP_MJ_CREATE](irp-mj-create.md)操作的 [FLT_PARAMETERS](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)结构包含由回调数据表示的基于 IRP 的 **创建** 操作的参数 ([FLT_CALLBACK_DATA](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)) 结构。 它包含在 [FLT_IO_PARAMETER_BLOCK](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block) 结构中。

IRP_MJ_CREATE 是基于 IRP 的操作。

## <a name="requirements"></a>要求

|标头 | *fltkernel* (包含 fltkernel) 

## <a name="see-also"></a>请参阅

[ACCESS_MASK](../kernel/access-mask.md)

[ACCESS_STATE](/windows-hardware/drivers/ddi/wdm/ns-wdm-_access_state)

[FILE_FULL_EA_INFORMATION](/windows-hardware/drivers/ddi/wdm/ns-wdm-_file_full_ea_information)

[FLT_CALLBACK_DATA](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_callback_data)

[FLT_IO_PARAMETER_BLOCK](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_io_parameter_block)

[FLT_IS_FASTIO_OPERATION](/windows-hardware/drivers/ddi/index)

[FLT_PARAMETERS](/windows-hardware/drivers/ddi/fltkernel/ns-fltkernel-_flt_parameters)

[**FltCreateFile**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatefile)

[IRP_MJ_CREATE](irp-mj-create.md)
