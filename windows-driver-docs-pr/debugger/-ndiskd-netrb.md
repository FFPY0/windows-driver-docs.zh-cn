---
title: ndiskd.netrb
description: Ndiskd. netrb 扩展显示 NET_RING 结构的相关信息。
keywords:
- ndiskd netrb Windows 调试
ms.date: 06/17/2020
topic_type:
- apiref
api_name:
- ndiskd.netrb
api_type:
- NA
ms.localizationpriority: medium
ms.custom: 19H1
ms.openlocfilehash: 262935598bff75a3d4dc27580ff1e9391fdf2d0b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834795"
---
# <a name="ndiskdnetrb"></a>!ndiskd.netrb

**！ Ndiskd netrb** 扩展显示有关 [网络 \_ 环形 \_ 缓冲区](/windows-hardware/drivers/ddi/ring/ns-ring-_net_ring)结构的信息。

有关网络适配器 WDF 类扩展的详细信息 (NetAdapterCx) ，请参阅 [网络适配器 Wdf Class extension (Cx) ](../netcx/index.md)。

```console
!ndiskd.netrb -handle <x> [-basic] [-dump] [-elementtype <str>] 
```

## <a name="parameters"></a>参数

<span id="_______-handle______"></span><span id="_______-HANDLE______"></span>*-handle*   
必需。 网络 \_ 环形缓冲区的地址 \_ 。

<span id="_______-basic______"></span><span id="_______-BASIC______"></span>*-基本*   
显示基本信息。

<span id="_______-dump______"></span><span id="_______-DUMP______"></span>*-dump*   
显示网络环形缓冲区中每个元素的相关信息 \_ \_ 。

<span id="_______-elementtype______"></span><span id="_______-ELEMENTTYPE______"></span>*-elementtype*   
引用环形缓冲区元素时要使用的数据类型的字符串。

### <a name="dll"></a>DLL

Ndiskd.dll

### <a name="examples"></a>示例

**注意** 若 [Summary of Objects](../netcx/summary-of-netadaptercx-objects.md)要查看 \_ \_ 与 NetAdapterCx 中的其他对象之间的网络环形缓冲对象关系的关系图，请参阅对象的摘要。

若要获取网络环形缓冲区的句柄 \_ \_ ，请执行以下步骤：

1. 运行 [**！ ndiskd. get-netadapter**](-ndiskd-netadapter.md) 扩展。
2. 单击安装了 NetAdapterCx 驱动程序的 Get-netadapter 的句柄。
3. 单击 Get-netadapter 的 GET-NETADAPTER 对象右侧的 "详细信息" 链接，以运行 [**！ ndiskd. cxadapter**](-ndiskd-cxadapter.md) 扩展。
4. 输入包含 *-数据路径* 参数的 **！ cxadapter** 命令，以查看 get-netadapter 的数据路径队列。
5. 单击其中一个数据路径队列的句柄。

有关此过程中步骤1-4 的详细信息，请参阅 **！ ndiskd. cxadapter** 主题中的示例。 有关此过程的步骤5的详细信息，请参阅《 [**！ ndiskd. netqueue**](-ndiskd-netqueue.md) 主题中的示例。
在下面的示例中，查找此 NETTXQUEUE 的环形缓冲区 ffffd1022d000000 的句柄。

```console
0: kd> !ndiskd.netqueue ffffd1022f512700

    NETTXQUEUE         00002efdd0aed9a8
    Ring buffer        ffffd1022d000000

    Switch to EC thread

    Event Callbacks                        Function pointer   Symbol (if available)
    EvtQueueAdvance                        fffff80034152af8   RtEthSample+2af8
    EvtQueueArmNotification                fffff80034159a94   RtEthSample+9a94
    EvtQueueCancel                         fffff800341598d8   RtEthSample+98d8
```

通过单击环形缓冲区的句柄，或在命令行上输入 **！ ndiskd** 命令，可以查看此网络环形缓冲区的详细信息 \_ ，包括该网络环形 \_ 缓冲区包含多少元素以及其开始和结束索引的地址。

```console
0: kd> !ndiskd.netrb ffffd1022d000000

    NET_RING    ffffd1022d000000

    Number of elements 0x080
    Owned by OS        0x080
    Owned by Client    00000

    Begin Index        0x078 (ffffd1022d003c40 - NET_PACKET)
    Next Index         0x078 (ffffd1022d003c40 - NET_PACKET)
    End Index          0x078 (ffffd1022d003c40 - NET_PACKET)

    List all elements
```

若要查看此网络 \_ 环形 \_ 缓冲区的元素，请单击其详细信息底部的 "列出所有元素" 链接，或在命令行上输入 **！ ndiskd** 命令。 下面的示例为简洁起见，excised 了中间元素。

```console
0: kd> !ndiskd.netrb ffffd1022d000000 -dump

    [000] ffffd1022d000040 - NET_PACKET
    [001] ffffd1022d0000c0 - NET_PACKET
    [002] ffffd1022d000140 - NET_PACKET
    [003] ffffd1022d0001c0 - NET_PACKET
    [004] ffffd1022d000240 - NET_PACKET
    [005] ffffd1022d0002c0 - NET_PACKET
    
    ...

    [07b] ffffd1022d003dc0 - NET_PACKET
    [07c] ffffd1022d003e40 - NET_PACKET
    [07d] ffffd1022d003ec0 - NET_PACKET
    [07e] ffffd1022d003f40 - NET_PACKET
    [07f] ffffd1022d003fc0 - NET_PACKET
```

## <a name="see-also"></a>请参阅

[网络驱动程序设计指南](../network/index.md)

[Windows Vista 和更高版本的网络引用](/windows-hardware/drivers/ddi/_netvista/)

[调试网络堆栈](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 扩展 ( # A0)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[网络适配器 WDF 类扩展 (Cx) ](../netcx/index.md)

[对象摘要](../netcx/summary-of-netadaptercx-objects.md)

[网络 \_ 环形 \_ 缓冲区](/windows-hardware/drivers/ddi/ring/ns-ring-_net_ring)

[**!ndiskd.netadapter**](-ndiskd-netadapter.md)

[**!ndiskd.cxadapter**](-ndiskd-cxadapter.md)

[**!ndiskd.netqueue**](-ndiskd-netqueue.md)
