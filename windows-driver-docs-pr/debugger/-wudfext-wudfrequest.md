---
title: wudfext.wudfrequest
description: Wudfext. wudfrequest 扩展显示有关 i/o 请求的信息。
keywords:
- wudfext wudfrequest Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- wudfext.wudfrequest
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 07947401d6440a6af7a0dd0f61b71c20a477b210
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838381"
---
# <a name="wudfextwudfrequest"></a>!wudfext.wudfrequest

**！ Wudfext wudfrequest** 扩展显示有关 i/o 请求的信息。

```dbgcmd
!wudfext.wudfrequest pWDFRequest
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters

<span id="_______pWDFRequest______"></span><span id="_______pwdfrequest______"></span><span id="_______PWDFREQUEST______"></span>*pWDFRequest*   
指定要显示其相关信息的 **WDFIoRequest** 接口的地址。 [**！ Wudfext wudfqueue**](-wudfext-wudfqueue.md) extension 命令确定 **WDFIoRequest** 的地址。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

Wudfext.dll
 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关详细信息，请参阅 [用户模式驱动程序框架调试](user-mode-driver-framework-debugging.md)。

<a name="remarks"></a>备注
-------

下面是 **！ wudfext** 显示的示例：

```dbgcmd
kd> !wudfrequest 0x000fa530 
CWdfIoRequest  0x000fa4b8
Type: WdfRequestRead
  IWDFIoQueue: 0x000f3500
Completed: No
Canceled: No
UM IRP: 0x00429108  UniqueId: 0xf4  Kernel Irp: 0x0x936ef160
  Type: WudfMsg_READ
  ClientProcessId: 0x1248
  Device Stack: 0x003be4e0
  IoStatus
    hrStatus: 0x0
    Information: 0x0
  Driver/Framework created IRP: No
  Data Buffer: 0x00000000 / 0
  IsFrom32BitProcess: Yes
  CancelFlagSet: No
  Cancel callback: 0x000fa534
  Total number of stack locations: 2
  CurrentStackLocation: 2 (StackLocation[ 1 ])
    StackLocation[ 0 ]
      UNINITIALIZED
  > StackLocation[ 1 ]
      IWDFRequest:  ????
      IWDFDevice:   0x000f2f80
      IWDFFile:     0x00418cf0
      Completion:
        Callback:   0x00000000
        Context:    0x00000000
      Parameters: (RequestType: WdfRequestRead)
        Buffer length:        0x400
        Key:                  0x00000000
        Offset:               0x0
```

 

 





