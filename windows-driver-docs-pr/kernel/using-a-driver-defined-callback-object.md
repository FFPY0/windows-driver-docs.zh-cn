---
title: 使用驱动程序定义的回调对象
description: 使用驱动程序定义的回调对象
keywords:
- 回叫对象 WDK 内核
- 驱动程序定义的回叫对象 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8b534c0cc09af07bf7856b596f201ef865e469e7
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827599"
---
# <a name="using-a-driver-defined-callback-object"></a>使用驱动程序定义的回调对象





若要使用另一驱动程序定义的回调对象，驱动程序会打开该对象，然后注册在触发回调时要调用的例程，如下图所示。 请求通知的驱动程序必须知道回调对象的名称，并且必须了解传递到回调例程的参数的语义。

![说明回调通知注册的示意图](images/3reg-cbk.png)

在打开对象之前，驱动程序必须调用 [**InitializeObjectAttributes**](/windows/win32/api/ntdef/nf-ntdef-initializeobjectattributes) 来创建属性块，并指定对象的名称。 在该指针指向属性块后，它将调用 [**ExCreateCallback**](/windows-hardware/drivers/ddi/wdm/nf-wdm-excreatecallback)，传递特性指针、要接收回调句柄的位置以及 *Create* 参数的 **FALSE** （表示它需要现有的回调对象）。

然后，该驱动程序可以调用 [**ExRegisterCallback**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exregistercallback) 和返回的句柄来注册其回调例程。

回调例程具有以下原型：

```cpp
typedef VOID (*PCALLBACK_FUNCTION ) (
    IN PVOID CallbackContext,
    IN PVOID Argument1,
    IN PVOID Argument2
    );
```

*CallbackContext* 参数是要在每次调用回调例程时传递到该例程的上下文指针。 通常，此参数是指向上下文数据块的指针，如果可以在调度级别调用例程，则调用方应从非分页池分配 \_ 。 这两个参数由创建回调的组件定义。 通常，参数提供有关触发回调的条件的信息。

当回调的创建者触发通知时，系统将调用注册的例程，同时传递指向上下文和两个自变量的指针。 自变量的值由创建回调的组件提供。 回调例程的调用位置与创建驱动程序触发通知的 IRQL 相同，后者始终为 IRQL &lt; = 调度 \_ 级别。

在其回调例程中，驱动程序可以执行当前条件所需的任何任务。

当驱动程序不再需要通知时，它应调用 [**ExUnregisterCallback**](/windows-hardware/drivers/ddi/wdm/nf-wdm-exunregistercallback) ，从注册的回调列表中删除其例程，并删除其对回调对象的引用。

 

