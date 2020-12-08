---
title: DispatchQueryInformation 例程
description: DispatchQueryInformation 例程
keywords:
- 调度例程 WDK 内核，DispatchQueryInformation 例程
- DispatchQueryInformation 例程
- IRP_MJ_QUERY_INFORMATION i/o 函数代码
- 查询信息发送例程 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: e97e0de2736b8e86ce803421a2d436b8b99daeb7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96825933"
---
# <a name="dispatchqueryinformation-routines"></a>DispatchQueryInformation 例程





驱动程序的 [*DispatchQueryInformation*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_dispatch) 例程为 [**irp \_ MJ \_ 查询 \_ 信息**](./irp-mj-query-information.md) i/o 函数代码处理 irp。 此 i/o 函数代码的驱动程序支持是可选的，通常出现在较高级别的或文件系统驱动程序中。 此请求由 i/o 管理器和其他操作系统组件以及其他内核模式驱动程序发送。 例如，在用户模式应用程序调用 [**GetFileInformationByHandle**](/windows/win32/api/fileapi/nf-fileapi-getfileinformationbyhandle)时，以及当内核模式组件调用 [**ZwQueryInformationFile**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntqueryinformationfile)时发送。

 

