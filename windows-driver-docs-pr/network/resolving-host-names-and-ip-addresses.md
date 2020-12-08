---
title: 解析主机名和 IP 地址
description: 解析主机名和 IP 地址
keywords:
- WSK WDK 网络，名称解析
- Winsock 内核 WDK 网络，名称解析
- 主机名称转换到传输地址 WDK Winsock 内核
- 向主机名称转换的传输地址 WDK Winsock 内核
- 传输地址 WDK Winsock 内核
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7bb2a44ac49a318d8e90f974965d7fc592ce79af
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813637"
---
# <a name="resolving-host-names-and-ip-addresses"></a>解析主机名和 IP 地址


从 Windows 7 开始， *内核名称解析* 功能允许内核模式组件在 Unicode 主机名和传输地址之间执行与协议无关的转换。 你可以使用以下 [Winsock 内核 (WSK) ](/windows-hardware/drivers/ddi/_netvista/) 客户端级功能来执行此名称解析：

-   [**WskFreeAddressInfo**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_free_address_info)

-   [**WskGetAddressInfo**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_get_address_info)

-   [**WskGetNameInfo**](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_get_name_info)

这些函数分别与用户模式函数 [**FreeAddrInfoW**](/windows/win32/api/ws2tcpip/nf-ws2tcpip-freeaddrinfow)、 [**GetAddrInfoW**](/windows/win32/api/ws2tcpip/nf-ws2tcpip-getaddrinfow)和 [**GetNameInfoW**](/windows/win32/api/ws2tcpip/nf-ws2tcpip-getnameinfow)执行名称地址转换。

若要利用此功能，必须使用 NTDDI \_ 版本宏设置为 NTDDI \_ WIN7 或更高版本来编译或重新编译该驱动程序。

为了使你的驱动程序使用内核名称解析功能，必须执行以下调用序列：

1.  调用 [**WskRegister**](/windows-hardware/drivers/ddi/wsk/nf-wsk-wskregister) 以注册到 WSK。

2.  调用 [**WskCaptureProviderNPI**](/windows-hardware/drivers/ddi/wsk/nf-wsk-wskcaptureprovidernpi) 捕获 WSK 提供程序 [网络编程接口 (NPI)](network-programming-interface.md)。

3.  使用 WSK 提供程序 NPI 完成后，调用 [**WskReleaseProviderNPI**](/windows-hardware/drivers/ddi/wsk/nf-wsk-wskreleaseprovidernpi) 以释放 WSK 提供程序 NPI。

4.  调用 [**WskDeregister**](/windows-hardware/drivers/ddi/wsk/nf-wsk-wskderegister) 取消注册 WSK 应用程序。

下面的代码示例使用上述调用序列来显示 WSK 应用程序如何调用 **WskGetAddressInfo** 函数以将主机名转换为传输地址。

```C++
NTSTATUS
SyncIrpCompletionRoutine(
    __in PDEVICE_OBJECT Reserved,
    __in PIRP Irp,
    __in PVOID Context
    )
{    
    PKEVENT compEvent = (PKEVENT)Context;
    UNREFERENCED_PARAMETER(Reserved);
    UNREFERENCED_PARAMETER(Irp);
    KeSetEvent(compEvent, 2, FALSE);    
    return STATUS_MORE_PROCESSING_REQUIRED;
}

NTSTATUS
KernelNameResolutionSample(
    __in PCWSTR NodeName,
    __in_opt PCWSTR ServiceName,
    __in_opt PADDRINFOEXW Hints,
    __in PWSK_PROVIDER_NPI WskProviderNpi
    )
{
    NTSTATUS status;
    PIRP irp;
    KEVENT completionEvent;
    UNICODE_STRING uniNodeName, uniServiceName, *uniServiceNamePtr;
    PADDRINFOEXW results;

    PAGED_CODE();
    //
    // Initialize UNICODE_STRING structures for NodeName and ServiceName 
    //
 
    RtlInitUnicodeString(&uniNodeName, NodeName);

    if(ServiceName == NULL) {
        uniServiceNamePtr = NULL;
    }
    else {
        RtlInitUnicodeString(&uniServiceName, ServiceName);
        uniServiceNamePtr = &uniServiceName;
    }

    //
    // Use an event object to synchronously wait for the 
    // WskGetAddressInfo request to be completed. 
    //
 
    KeInitializeEvent(&completionEvent, SynchronizationEvent, FALSE);

    //
    // Allocate an IRP for the WskGetAddressInfo request, and set the 
    // IRP completion routine, which will signal the completionEvent
    // when the request is completed.
    //
 
    irp = IoAllocateIrp(1, FALSE);
    if(irp == NULL) {
        return STATUS_INSUFFICIENT_RESOURCES;
    }        

    IoSetCompletionRoutine(irp, SyncIrpCompletionRoutine, 
  &completionEvent, TRUE, TRUE, TRUE);

    //
    // Make the WskGetAddressInfo request.
    //
 
    WskProviderNpi->Dispatch->WskGetAddressInfo (
        WskProviderNpi->Client,
        &uniNodeName,
        uniServiceNamePtr,
        NS_ALL,
        NULL, // Provider
        Hints,
        &results, 
        NULL, // OwningProcess
        NULL, // OwningThread
        irp);

    //
    // Wait for completion. Note that processing of name resolution results
    // can also be handled directly within the IRP completion routine, but
    // for simplicity, this example shows how to wait synchronously for 
    // completion.
    //
 
    KeWaitForSingleObject(&completionEvent, Executive, 
                        KernelMode, FALSE, NULL);

    status = irp->IoStatus.Status;

    IoFreeIrp(irp);

    if(!NT_SUCCESS(status)) {
        return status;
    }

    //
    // Process the name resolution results by iterating through the addresses
    // within the returned ADDRINFOEXW structure.
    //
 
   results; // your code here

    //
    // Release the returned ADDRINFOEXW structure when no longer needed.
    //
 
    WskProviderNpi->Dispatch->WskFreeAddressInfo(
        WskProviderNpi->Client,
        results);

    return status;
} 
```

 

