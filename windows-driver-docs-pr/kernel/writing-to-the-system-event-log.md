---
title: 写入到系统事件日志
description: 写入到系统事件日志
keywords:
- NTSTATUS 值 WDK 内核
- 转储数据 WDK 内核
- 预定义错误代码 WDK 内核
- 系统事件日志 WDK 内核
- 属性表 WDK 错误
- 事件查看器 WDK 内核
- 示例日志条目属性表 WDK 内核
- 日志条目 WDK 内核
- 输入 WDK 错误日志
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5924364c3df10b51b8f7f670ec187ad98b9eaae9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782579"
---
# <a name="writing-to-the-system-event-log"></a>写入到系统事件日志





错误由其 NTSTATUS 值指定。 系统预定义驱动程序可以使用的特定 NTSTATUS 值，驱动程序编写器可以定义其他错误。 请注意，在记录错误时，只能使用某些 NTSTATUS 值。

记录错误时可以使用的每个 NTSTATUS 值都有关联的错误消息。 例如，并行端口驱动程序使用 NTSTATUS 值 PAR \_ 中断 \_ 冲突来表示硬件中断冲突，并显示消息文本 "检测到 %1 的中断冲突"。

事件查看器在日志条目的属性表上的 " **描述** " 文本框中显示消息文本。 如果消息文本字符串包含 "%1"，则事件查看器会将其替换为记录该项的设备的名称。 消息文本可以包含 "%2"、"%3" 等 "格式" 的其他参数。 当驱动程序记录错误时，它可以提供这些参数的字符串值。 这些字符串值称为 *插入字符串*。 事件查看器将自动插入它们来代替百分比值。

驱动程序还可以在日志条目中包含二进制数据（称为 *转储数据*）。 事件查看器在日志条目的属性表的 " **数据** " 文本框中显示转储数据。

通过双击 "事件查看器中的条目，可以打开日志条目的属性表。 下面的屏幕截图显示了一个示例日志条目属性表。

![事件属性表的屏幕截图](images/event-properties.png)

驱动程序使用 [**IoAllocateErrorLogEntry**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioallocateerrorlogentry) 例程来分配错误日志项。 日志条目由可变长度 [**IO \_ 错误 \_ 日志 \_ 数据包**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_error_log_packet) 标头组成，后跟插入字符串。

下图显示内存中错误日志条目的布局。

![说明内存中错误日志数据包布局的关系图 ](images/errorlogentry.png)

**IO \_ 错误 \_ 日志 \_ 数据包** 的 **ErrorCode** 成员指定错误的 NTSTATUS 值。 **DumpData** 成员为日志条目指定任何转储数据。 **DumpData** 是一个可变大小的数组，其大小由 **DumpDataSize** 成员指定。 驱动程序指定第一个插入字符串与 **StringOffset** 成员的开头，并指定 **NumberOfStrings** 成员中字符串的数目。 每个插入字符串本身均为以 null 结尾的 Unicode 字符串。

一旦驱动程序填写了 "已分配错误日志" 条目，它将使用 [**IoWriteErrorLogEntry**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-iowriteerrorlogentry)将条目写入错误日志。 **IoWriteErrorLogEntry** 自动释放为日志条目分配的内存。 驱动程序可以使用 [**IoFreeErrorLogEntry**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iofreeerrorlogentry) 来释放任何未使用的日志条目。

格式为 IO ERR XXX) 的预定义错误 (代码 \_ \_ *XXX* 在 ntiologc 头文件中定义，该文件包含在 Windows 驱动程序工具包 (WDK) 中。 与每个错误代码相关联的错误消息可在错误代码声明旁的 ntiologc 注释中找到。 若要使用预定义的错误代码，驱动程序必须将系统文件（iologmsg.dll）注册为关联的错误消息的源。 有关详细信息，请参阅 [注册为错误消息源](registering-as-a-source-of-error-messages.md)。

驱动程序还可以定义自己的自定义错误类型和相关的错误消息。 有关详细信息，请参阅 [定义自定义错误类型](defining-custom-error-types.md)。

 

