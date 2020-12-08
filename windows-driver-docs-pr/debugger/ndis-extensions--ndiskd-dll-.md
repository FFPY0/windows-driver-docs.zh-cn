---
title: NDIS 扩展 (Ndiskd.dll)
description: NDIS 扩展 (Ndiskd.dll)
keywords:
- 'NDIS 扩展 ( # A0) '
- 'ndiskd.dll (NDIS 扩展) '
- 扩展，NDIS
ms.date: 06/29/2020
ms.localizationpriority: medium
ms.openlocfilehash: 475ad2c18f366e3b114a0c8926af2e2dacee0570
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831949"
---
# <a name="ndis-extensions-ndiskddll"></a>NDIS 扩展 (Ndiskd.dll)

## <span id="ddk_ndis_extensions_ndiskd_dll__dbg"></span><span id="DDK_NDIS_EXTENSIONS_NDISKD_DLL__DBG"></span>

本部分介绍！ ndiskd 中可用的命令，它是一个可用于调试 NDIS (网络设备接口规范) 驱动程序的调试器扩展。 网络驱动程序开发人员可以使用这些命令来查看 Windows 网络堆栈的更大的图片以及其驱动程序与之进行交互的方式。 使用！ ndiskd，你可以查看 ([**！ ndiskd get-netadapter**](-ndiskd-netadapter.md)) 的所有网络适配器的状态、计算机网络堆栈的可视化关系图 ([**！ ndiskd**](-ndiskd-netreport.md)) 、网络适配器上的流量日志 ([**！ netreport**](-ndiskd-nbllog.md)) ，或 ([**！ ndiskd**](-ndiskd-oid.md)) 的所有挂起的 OID 请求的列表。

可在 Ndiskd.dll 中找到命令。 若要加载符号，请在调试器命令窗口中输入 **. reload.sql/f ndis.sys** 。 若要确认符号是否已成功加载，请使用 [**！ lmi ndis**](-lmi.md) 扩展，并在底部查找 "已成功加载的符号" 字样。 输出应类似于以下示例：

```dbgcmd
0: kd> !lmi ndis
Loaded Module Info: [ndis] 
         Module: ndis
   Base Address: fffff80174570000
     Image Name: ndis.sys
   Machine Type: 34404 (X64)
     Time Stamp: 938f9f4e (This is a reproducible build file hash, not a true timestamp)
           Size: 16f000
       CheckSum: 167a05
Characteristics: 22  
Debug Data Dirs: Type  Size     VA  Pointer
             CODEVIEW    21, d4060,   d2c60 RSDS - GUID: {9CC82DBE-96A0-773D-29E0-62B698C4C3A8}
               Age: 1, Pdb: ndis.pdb
                 POGO   988, d4084,   d2c84 [Data not mapped]
                REPRO    24, d4a0c,   d360c Reproducible build[Data not mapped]
     Image Type: MEMORY   - Image read successfully from loaded memory.
    Symbol Type: PDB      - Symbols loaded successfully from symbol server.
                 C:\ProgramData\Dbg\sym\ndis.pdb\9CC82DBE96A0773D29E062B698C4C3A81\ndis.pdb
    Load Report: public symbols , not source indexed 
                 C:\ProgramData\Dbg\sym\ndis.pdb\9CC82DBE96A0773D29E062B698C4C3A81\ndis.pdb
```

## <a name="span-id_ndiskd_hyperlinksspanspan-id_ndiskd_hyperlinksspanspan-id_ndiskd_hyperlinksspanndiskd-hyperlinks"></a><span id="_ndiskd_Hyperlinks"></span><span id="_ndiskd_hyperlinks"></span><span id="_NDISKD_HYPERLINKS"></span>！ ndiskd 超链接

！ Ndiskd 中的许多扩展命令向你显示其在调试器窗口中显示的结果中的超链接。 这些超链接的文本保留在提供的示例中，以说明在调试对象计算机上运行命令时将看到的确切格式。 其中一些示例还显式地引用了这些链接，以便您可以了解典型的使用流，尽管示例还提供了每个命令的备用命令行形式。

## <a name="span-idcommon_parametersspanspan-idcommon_parametersspanspan-idcommon_parametersspancommon-parameters"></a><span id="Common_Parameters"></span><span id="common_parameters"></span><span id="COMMON_PARAMETERS"></span>通用参数

All！ ndiskd 命令支持以下泛型参数。

<span id="_______-verbose______"></span><span id="_______-VERBOSE______"></span>*-verbose*   
显示其他详细信息。

<span id="_______-terse______"></span><span id="_______-TERSE______"></span>*-简要*   
禁止显示某些样本输出。

<span id="_______-static______"></span><span id="_______-STATIC______"></span>*-static*   
禁止显示某些交互式输出。

<span id="_______-dml_0_1______"></span><span id="_______-DML_0_1______"></span>*-dml 0 | 1*   
控制是否启用 DML (调试器标记语言) 输出。

<span id="_______-unicode_0_1______"></span><span id="_______-UNICODE_0_1______"></span>*-unicode 0 | 1*   
控制是否允许 Unicode 字符输出。

<span id="_______-indent_N______"></span><span id="_______-indent_n______"></span><span id="_______-INDENT_N______"></span>*-缩进 N*   
每个缩进级别使用 *N* 个空格。

<span id="_______-force______"></span><span id="_______-FORCE______"></span>*-force*   
覆盖对远程数据稳定的某些安全检查。

<span id="_______-tracedata______"></span><span id="_______-TRACEDATA______"></span>*-tracedata*   
显示要调试的详细跟踪消息！ ndiskd 本身。

## <a name="span-idnet_adapter__ndis_driver__and_general_commandsspanspan-idnet_adapter__ndis_driver__and_general_commandsspanspan-idnet_adapter__ndis_driver__and_general_commandsspannet-adapter-ndis-driver-and-general-commands"></a><span id="Net_Adapter__NDIS_Driver__and_General_Commands"></span><span id="net_adapter__ndis_driver__and_general_commands"></span><span id="NET_ADAPTER__NDIS_DRIVER__AND_GENERAL_COMMANDS"></span>Net Adapter、NDIS 驱动程序和常规命令


以下命令显示有关计算机的网络适配器、网络驱动程序和与网络堆栈 (相关的常规命令的信息，如 rcvqueues、打开、筛选器、Oid 和 RW 锁) 。

-   [**!ndiskd.netadapter**](-ndiskd-netadapter.md)
-   [**!ndiskd.minidriver**](-ndiskd-minidriver.md)
-   [**!ndiskd.rcvqueue**](-ndiskd-rcvqueue.md)
-   [**!ndiskd.protocol**](-ndiskd-protocol.md)
-   [**!ndiskd.mopen**](-ndiskd-mopen.md)
-   [**!ndiskd.filter**](-ndiskd-filter.md)
-   [**!ndiskd.filterdriver**](-ndiskd-filterdriver.md)
-   [**!ndiskd.oid**](-ndiskd-oid.md)
-   [**!ndiskd.ndisrwlock**](-ndiskd-ndisrwlock.md)
-   [**!ndiskd.netreport**](-ndiskd-netreport.md)

## <a name="span-idnet_buffer_list_and_net_buffer_commandsspanspan-idnet_buffer_list_and_net_buffer_commandsspanspan-idnet_buffer_list_and_net_buffer_commandsspannet_buffer_list-and-net_buffer-commands"></a><span id="NET_BUFFER_LIST_and_NET_BUFFER_Commands"></span><span id="net_buffer_list_and_net_buffer_commands"></span><span id="NET_BUFFER_LIST_AND_NET_BUFFER_COMMANDS"></span>NET \_ buffer \_ LIST 和 Net \_ buffer 命令


以下命令显示与 [**网络 \_ 缓冲区 \_ 列表**](../network/net-buffer-list-structure.md) 和 [**网络 \_ 缓冲区**](../network/net-buffer-structure.md) 结构有关的信息。

- [**!ndiskd.nbl**](-ndiskd-nbl.md)
- [**!ndiskd.nb**](-ndiskd-nb.md)
- [**!ndiskd.nblpool**](-ndiskd-nblpool.md)
- [**!ndiskd.nbpool**](-ndiskd-nbpool.md)
- [**!ndiskd.pendingnbls**](-ndiskd-pendingnbls.md)
- [**!ndiskd.nbllog**](-ndiskd-nbllog.md)

## <a name="span-idnetadaptercx_commandsspanspan-idnetadaptercx_commandsspanspan-idnetadaptercx_commandsspannetadaptercx-commands"></a><span id="NetAdapterCx_Commands"></span><span id="netadaptercx_commands"></span><span id="NETADAPTERCX_COMMANDS"></span>NetAdapterCx 命令

以下命令显示与网络适配器 WDF 类 Extension [NetAdapterCx](../netcx/index.md) 及其关联结构 [NET_RING_BUFFER](../netcx/introduction-to-net-rings.md) 和 [NET_PACKET](/windows-hardware/drivers/ddi/packet/ns-packet-_net_packet)相关的信息。

- [**!ndiskd.cxadapter**](-ndiskd-cxadapter.md)
- [**!ndiskd.netqueue**](-ndiskd-netqueue.md)
- [**!ndiskd.netrb**](-ndiskd-netrb.md)
- [**!ndiskd.netpacket**](-ndiskd-netpacket.md)
- [**!ndiskd.netfragment**](-ndiskd-netfragment.md)
- [**!ndiskd.nrc**](-ndiskd-nrc.md)
- [**!ndiskd.netring**](-ndiskd-netring.md)

## <a name="span-idnetwork_interface_commandsspanspan-idnetwork_interface_commandsspanspan-idnetwork_interface_commandsspannetwork-interface-commands"></a><span id="Network_Interface_Commands"></span><span id="network_interface_commands"></span><span id="NETWORK_INTERFACE_COMMANDS"></span>网络接口命令

以下命令显示与网络接口相关的信息。

- [**!ndiskd.interfaces**](-ndiskd-interfaces.md)
- [**!ndiskd.ifprovider**](-ndiskd-ifprovider.md)

## <a name="span-idndis_packet_commandsspanspan-idndis_packet_commandsspanspan-idndis_packet_commandsspanndis_packet-commands"></a><span id="NDIS_PACKET_Commands"></span><span id="ndis_packet_commands"></span><span id="NDIS_PACKET_COMMANDS"></span>NDIS \_ 数据包命令

以下命令显示有关 [NDIS \_ 数据包](/previous-versions/windows/hardware/network/ff557086(v=vs.85)) 结构的信息。 这些扩展适用于旧的 NDIS 1.x 驱动程序。 NDIS \_ 数据包结构及其关联的体系结构已弃用。

- [**!ndiskd.pkt**](-ndiskd-pkt.md)
- [**!ndiskd.pktpools**](-ndiskd-pktpools.md)
- [**!ndiskd.findpacket**](-ndiskd-findpacket.md)

## <a name="span-idcondis_commandsspanspan-idcondis_commandsspanspan-idcondis_commandsspancondis-commands"></a><span id="CoNDIS_Commands"></span><span id="condis_commands"></span><span id="CONDIS_COMMANDS"></span>CoNDIS 命令

以下命令显示有关 [面向连接的 NDIS](../network/connection-oriented-ndis.md) 连接的信息。

- [**!ndiskd.vc**](-ndiskd-vc.md)
- [**!ndiskd.af**](-ndiskd-af.md)

## <a name="span-idndis_debugging_commandsspanspan-idndis_debugging_commandsspanspan-idndis_debugging_commandsspanndis-debugging-commands"></a><span id="NDIS_Debugging_Commands"></span><span id="ndis_debugging_commands"></span><span id="NDIS_DEBUGGING_COMMANDS"></span>NDIS 调试命令

以下命令显示与 NDIS refcounts、事件日志、堆栈跟踪和调试跟踪相关的信息。

- [**!ndiskd.ndisref**](-ndiskd-ndisref.md)
- [**!ndiskd.ndisevent**](-ndiskd-ndisevent.md)
- [**!ndiskd.ndisstack**](-ndiskd-ndisstack.md)
- [**!ndiskd.dbglevel**](-ndiskd-dbglevel.md)
- [**!ndiskd.dbgsystems**](-ndiskd-dbgsystems.md)

## <a name="span-idwdi_commandsspanspan-idwdi_commandsspanspan-idwdi_commandsspanwdi-commands"></a><span id="WDI_Commands"></span><span id="wdi_commands"></span><span id="WDI_COMMANDS"></span>WDI 命令

以下命令显示有关 [WDI 微型端口驱动程序](../network/wdi-miniport-driver-design-guide.md)的信息。

- [**!ndiskd.wdiadapter**](-ndiskd-wdiadapter.md)
- [**!ndiskd.wdiminidriver**](-ndiskd-wdiminidriver.md)
- [**!ndiskd.nwadapter**](-ndiskd-nwadapter.md)

## <a name="span-idndis_and__ndiskd_information_commandsspanspan-idndis_and__ndiskd_information_commandsspanspan-idndis_and__ndiskd_information_commandsspanndis-and-ndiskd-information-commands"></a><span id="NDIS_and__ndiskd_Information_Commands"></span><span id="ndis_and__ndiskd_information_commands"></span><span id="NDIS_AND__NDISKD_INFORMATION_COMMANDS"></span>NDIS 和！ ndiskd 信息命令

以下命令显示有关 NDIS.sys 和 ndiskd.dll 的信息。

- [**!ndiskd.ndis**](-ndiskd-ndis.md)
- [**!ndiskd.ndiskdversion**](-ndiskd-ndiskdversion.md)

## <a name="span-idmiscellaneous_commandsspanspan-idmiscellaneous_commandsspanspan-idmiscellaneous_commandsspanmiscellaneous-commands"></a><span id="Miscellaneous_Commands"></span><span id="miscellaneous_commands"></span><span id="MISCELLANEOUS_COMMANDS"></span>其他命令

- [**!ndiskd.ifstacktable**](-ndiskd-ifstacktable.md)
- [**!ndiskd.compartments**](-ndiskd-compartments.md)
- [**!ndiskd.ndisslot**](-ndiskd-ndisslot.md)

## <a name="span-idrelated_topicsspanspan-idrelated_topicsspanspan-idrelated_topicsspanrelated-topics"></a><span id="Related_Topics"></span><span id="related_topics"></span><span id="RELATED_TOPICS"></span>相关主题

有关设计适用于 Windows Vista 和更高版本的 NDIS 驱动程序的详细信息，请参阅 [网络驱动程序设计指南](../network/index.md)。

有关适用于 Windows Vista 和更高版本的 NDIS 驱动程序参考的详细信息，请参阅 [Windows vista 和更高版本的网络参考](/windows-hardware/drivers/ddi/_netvista/)。

有关使用！ ndiskd 调试器命令调试网络堆栈的演示，请参阅 [调试网络 stack](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack) 第9频道视频。
