---
title: ndiskd.nrc
description: Ndiskd. nrc 扩展显示 NET_PACKET_FRAGMENT 结构的相关信息。
keywords:
- ndiskd nrc Windows 调试
ms.date: 06/17/2020
topic_type:
- apiref
api_name:
- ndiskd.nrc
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c9e212a11429a126a2821586201b00e4adc5f9e3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808535"
---
# <a name="ndiskdnrc"></a>!ndiskd.nrc

**！ Ndiskd. nrc** 扩展显示有关 [网络 \_ 环 \_ 集合](/windows-hardware/drivers/ddi/ringcollection/ns-ringcollection-_net_ring_collection)结构的信息。

有关网络适配器 WDF 类扩展的详细信息 (NetAdapterCx) ，请参阅 [网络适配器 Wdf 类扩展 (Cx) ](../netcx/index.md) 和 [网络环简介](../netcx/introduction-to-net-rings.md)。

```console
!ndiskd.nrc -handle <x> [-basic] [-packet] [-fragment] [-dump]
```

## <a name="parameters"></a>参数

*-handle*    
必需。 网络 \_ 振铃收集的 \_ 地址

*-基本*    
显示数据包环和片段环的链接。

*-数据包*     
仅显示数据包环的内容。

*-片段*     
仅显示片段圆圈内容。

*-dump*     
显示有关每个元素 (包/片段) 的信息。

### <a name="dll"></a>DLL

Ndiskd.dll

### <a name="examples"></a>示例

**注意**  请参阅 [对象摘要](../netcx/summary-of-netadaptercx-objects.md) ，以查看说明网络 \_ 数据包对象与 NetAdapterCx 中的其他对象的关系的关系图。

若要获取网络数据包的句柄 \_ ，请执行以下步骤：

1. 运行 [**！ ndiskd. get-netadapter**](-ndiskd-netadapter.md) 扩展。
2. 单击安装了 NetAdapterCx 驱动程序的 Get-netadapter 的句柄。
3. 单击 Get-netadapter 的 GET-NETADAPTER 对象右侧的 "详细信息" 链接，以运行 [**！ ndiskd. cxadapter**](-ndiskd-cxadapter.md) 扩展。
4. 输入包含 *-数据路径* 参数的 **！ cxadapter** 命令，以查看 get-netadapter 的数据路径队列。
5. 单击其中一个数据路径队列的句柄。
6. 单击该数据路径队列的环形缓冲区的句柄。 待定-这是否适用于 nrc？
7. 单击环形缓冲区详细信息底部的 "列出所有元素" 链接，查看其包含的元素。 TBD TBD 待定
8. 单击其中一个 "网络 \_ 环" \_ 集合对象 TBD。

有关此过程中步骤1-4 的详细信息，请参阅 **！ ndiskd. cxadapter** 主题中的示例。 有关此过程的步骤5的详细信息，请参阅《 [**！ ndiskd. netqueue**](-ndiskd-netqueue.md) 主题中的示例。 有关此过程中步骤6-7 的详细信息，请参阅 [**！ ndiskd. netrb**](-ndiskd-netrb.md) 主题中的示例。

在下面的示例中，查找此网络环集合的 TBD 的句 \_ 柄 \_ ，ffffffTBDffffffffff。

```console
0: kd> !ndiskd.nrc ffffffTBDffffffffff


TBD

TBD

TBD

```

此示例演示如何使用-packet 选项，并显示 TBD。

```console
0: kd> !ndiskd.nrc ffffffTBDffffffffff -packet

TBD

TBD

TBD

```

此示例演示如何使用-片断 (或 dump？ TBD) 选项，并显示 TBD。

```console
0: kd> !ndiskd.nrc ffffffTBDffffffffff -fragment

TBD

TBD

TBD

```

## <a name="see-also"></a>请参阅

[网络驱动程序设计指南](../network/index.md)

[Windows Vista 和更高版本的网络引用](/windows-hardware/drivers/ddi/_netvista/)

[调试网络堆栈](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 扩展 ( # A0)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[网络适配器 WDF 类扩展 (Cx) ](../netcx/index.md)

[对象摘要](../netcx/summary-of-netadaptercx-objects.md)

[网络 \_ 振铃 \_ 收集](/windows-hardware/drivers/ddi/ringcollection/ns-ringcollection-_net_ring_collection)

[**!ndiskd.netadapter**](-ndiskd-netadapter.md)

[**!ndiskd.cxadapter**](-ndiskd-cxadapter.md)

[**!ndiskd.netqueue**](-ndiskd-netqueue.md)

[**!ndiskd.netrb**](-ndiskd-netrb.md)

[**!ndiskd.netpacket**](-ndiskd-netpacket.md)
