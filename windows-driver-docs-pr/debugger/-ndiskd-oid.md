---
title: ndiskd
description: Ndiskd 扩展显示有关 NDIS OID 请求的信息。
keywords:
- ndiskd Windows 调试
ms.date: 06/26/2020
topic_type:
- apiref
api_name:
- ndiskd.oid
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 609ce942c0e87374aa6d47e896caf4e8de0055d1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808529"
---
# <a name="ndiskdoid"></a>!ndiskd.oid

**！ Ndiskd** 扩展显示有关 NDIS oid 请求的信息。 如果运行不带参数的此扩展，！ ndiskd 将显示所有微型端口和筛选器上所有挂起的 OID 请求的列表。 每个微型端口或筛选器最多有一个挂起的 OID 请求和任意数量的排队 OID 请求。

请注意，筛选器通常会克隆 OID 请求并将克隆向下传递。 这意味着，即使某个协议发出单个 OID 请求，也可能存在多个克隆请求的实例：每个筛选器中有一个，另一个在小型端口中。 **！ ndiskd** 将单独显示每个克隆，因此你可能会看到比实际发出的协议更多的挂起 oid。

```console
!ndiskd.oid [-handle <x>] [-legacyoid] [-nolimit>] [-miniport <x>] 
```

## <a name="parameters"></a>参数

<span id="_______-handle______"></span><span id="_______-HANDLE______"></span>*-handle*   
NDIS \_ OID 请求的句 \_ 柄

<span id="_______-legacyoid______"></span><span id="_______-LEGACYOID______"></span>*-legacyoid*   
将视为传统 NDIS \_ 请求，而不是 NDIS \_ OID \_ 请求。

<span id="_______-nolimit______"></span><span id="_______-NOLIMIT______"></span>*-nolimit*   
不限制显示的挂起 Oid 的数目。

<span id="_______-miniport______"></span><span id="_______-MINIPORT______"></span>*-微型端口*   
查找此小型端口堆栈上的挂起 OID 请求。

### <a name="dll"></a>DLL

Ndiskd.dll

### <a name="remarks"></a>备注

**！ ndiskd** 每次显示系统上所有挂起的 oid 的列表，因此在调试系统挂起或 [0x9F bug 检查](bug-check-0x9f--driver-power-state-failure.md) 情况时，可能会有帮助， (驱动程序 \_ 电源 \_ 状态 \_ 故障) 。 例如，假设分析了一个虚构的 0x9F bug 检查，其中显示系统在 IRP 上挂起并等待 NDIS。 在 NDIS 中，将操作系统中的 Irp 转换为 Oid （包括电源转换），因此通过运行 **！ ndiskd** ，可以看到，在此示例中，堆栈底部的设备可能已 Clinging 到 [oid \_ PNP \_ 集 \_ 电源](../network/oid-pnp-set-power.md) ，并挂起堆栈的其余部分。 NDIS 驱动程序不应挂起 OID 超过一秒，因此，您可以在此之后调查为什么该设备保留 OID 的时间太长而无法尝试解决问题。

### <a name="examples"></a>示例

若要查看正常运行的系统上的挂起 OID 的示例，请在微型端口的对应微型端口驱动程序中 () 设置一个断点。 首先，运行不带参数的 [**！ ndiskd**](-ndiskd-minidriver.md) 命令，以获取系统上的微型端口驱动程序列表。 在此示例输出中，查找 kdnic 微型驱动程序，ffffdf801418d650 的句柄。

```console
3: kd> !ndiskd.minidriver
    ffffdf8015a98380 - tunnel
    ffffdf801418d650 - kdnic
```

单击微型驱动程序的句柄，并单击其详细信息页底部的 "处理程序" 链接，以查看其处理程序的列表。 您也可以输入 **！ ndiskd** 命令。 获得微型驱动程序的处理程序的列表后，请在此示例中查找 OidRequestHandler，其句柄为 fffff80f1fd71c90。

```console
2: kd> !ndiskd.minidriver ffffdf801418d650 -handlers


HANDLERS

    NDIS Handler                           Function pointer   Symbol (if available)
    InitializeHandlerEx                    fffff80f1fd78230  bp
    SetOptionsHandler                      fffff80f1fd72800  bp
    HaltHandlerEx                          fffff80f1fd78040  bp
    ShutdownHandlerEx                      fffff80f1fd722c0  bp

    CheckForHangHandlerEx                  fffff80f1fd72810  bp
    ResetHandlerEx                         fffff80f1fd72f70  bp

    PauseHandler                           fffff80f1fd78000  bp
    RestartHandler                         fffff80f1fd78940  bp

    OidRequestHandler                      fffff80f1fd71c90  bp
    CancelOidRequestHandler                fffff80f1fd722c0  bp
    DirectOidRequestHandler                [None]
    CancelDirectOidRequestHandler          [None]
    DevicePnPEventNotifyHandler            fffff80f1fd789a0  bp

    SendNetBufferListsHandler              fffff80f1fd71870  bp
    ReturnNetBufferListsHandler            fffff80f1fd71b50  bp
    CancelSendHandler                      fffff80f1fd722c0  bp
```

现在，单击 "OidRequestHandler" 右侧的 "最佳实践" 链接，或输入 [**最佳**](bp--bu--bm--set-breakpoint-.md) 方法，并在该例程上设置断点。 接下来，键入 **g** 命令，以允许调试对象目标计算机运行并命中刚刚设置的断点。

```console
2: kd> bp fffff80f1fd71c90
2: kd> g
Breakpoint 1 hit
fffff80f`1fd71c90 448b4204        mov     r8d,dword ptr [rdx+4]
```

在微型驱动程序的 OID 请求处理程序例程上触发断点（如上一示例所示）后，可以运行！ ndiskd 命令以查看系统上所有挂起的 Oid 的列表。

```console
1: kd> !ndiskd.oid


ALL PENDING OIDs

    NetAdapter         ffffdf80140c71a0 - Microsoft Kernel Debug Network Adapter
        Current OID        OID_GEN_STATISTICS
    Filter             ffffdf8014950c70 - Microsoft Kernel Debug Network Adapter-WFP Native MAC Layer LightWeight Filter-0000
        Current OID        OID_GEN_STATISTICS
    Filter             ffffdf801494dc70 - Microsoft Kernel Debug Network Adapter-QoS Packet Scheduler-0000
        Current OID        OID_GEN_STATISTICS
```

在此示例中，OID 搁置是 [oid \_ 生成 \_ 统计信息](../network/oid-gen-statistics.md)。 查看！ ndiskd 的结果时，请记住，筛选克隆 OID 请求并沿堆栈向下传递这些请求，Oid 通常会从筛选器传递到筛选器以筛选到小型端口。 因此，虽然在此示例中可能有三个具有相同名称的单独 OID 请求，但实际上有一个逻辑操作发生在物理上跨3个 Oid 和3个驱动程序。

## <a name="see-also"></a>请参阅

[网络驱动程序设计指南](../network/index.md)

[Windows Vista 和更高版本的网络引用](/windows-hardware/drivers/ddi/_netvista/)

[调试网络堆栈](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 扩展 ( # A0)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)

[0x9F bug 检查](bug-check-0x9f--driver-power-state-failure.md)

[OID \_ PNP \_ 设置 \_ 电源](../network/oid-pnp-set-power.md)

[**bp、bu、bm（设置断点）**](bp--bu--bm--set-breakpoint-.md)

[OID \_ 生成 \_ 统计信息](../network/oid-gen-statistics.md)

[NDIS Oid](/windows-hardware/drivers/ddi/_netvista/)

[NDIS OID 请求接口](/windows-hardware/drivers/ddi/_netvista/)
