---
title: 管理筛选层标识符
description: 本部分介绍管理筛选层标识符。
keywords:
- 管理筛选层标识符网络驱动程序
ms.date: 11/08/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9267042ceb42e9c992c7e573c3d1fd8fa2eef87
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96832207"
---
# <a name="management-filtering-layer-identifiers"></a>管理筛选层标识符

管理筛选层标识符通常由用户模式应用程序使用，每个都由 GUID （大小为128位）表示。 这些标识符的定义如下。

> [!NOTE]
> 层标识符末尾的 V4 和 V6 后缀指示该层是位于 IPv4 网络堆栈中还是位于 IPv6 网络堆栈中。

| 管理筛选层标识符 | 筛选层描述 |
| --- | --- |
| <p>FWPM_LAYER_INBOUND_IPPACKET_V4</p><p>FWPM_LAYER_INBOUND_IPPACKET_V6</p> | 此筛选层位于接收路径中，刚好在分析收到的数据包的 IP 标头之后、发生任何 IP 标头处理之前。 未发生 IPsec 解密或重新组合。 |
| <p>FWPM_LAYER_INBOUND_IPPACKET_V4_DISCARD</p><p>FWPM_LAYER_INBOUND_IPPACKET_V6_DISCARD</p> | 此筛选层位于接收路径中，用于处理已在网络层丢弃的任何已接收的数据包。 |
| <p>FWPM_LAYER_OUTBOUND_IPPACKET_V4</p><p>FWPM_LAYER_OUTBOUND_IPPACKET_V6</p> | 此筛选层位于发送路径中，刚好在对发送的数据包进行碎片计算之前。 所有 IP 标头处理已完成，并且所有扩展标头都已准备就绪。 已进行 IPsec 身份验证和加密。 |
| <p>FWPM_LAYER_OUTBOUND_IPPACKET_V4_DISCARD</p><p>FWPM_LAYER_OUTBOUND_IPPACKET_V6_DISCARD</p> | 此筛选层位于发送路径中，用于处理已在网络层丢弃的任何已发送的数据包。 |
| <p>FWPM_LAYER_IPFORWARD_V4</p><p>FWPM_LAYER_IPFORWARD_V6</p> | 此筛选层位于转发路径中接收的数据包转发到的位置。 |
| <p>FWPM_LAYER_IPFORWARD_V4_DISCARD</p><p>FWPM_LAYER_IPFORWARD_V6_DISCARD</p> | 此筛选层位于转发路径中，用于处理已在转发层上丢弃的任何转发的数据包。 |
| <p>FWPM_LAYER_INBOUND_TRANSPORT_V4</p><p>FWPM_LAYER_INBOUND_TRANSPORT_V6</p> | 在传输层上的网络堆栈对接收的数据包标头进行分析后，但在发生任何传输层处理之前，此筛选层位于接收路径中。 |
| <p>FWPM_LAYER_INBOUND_TRANSPORT_V4_DISCARD</p><p>FWPM_LAYER_INBOUND_TRANSPORT_V6_DISCARD</p> | 此筛选层位于接收路径中，用于处理在传输层被丢弃的任何已接收的数据包。 |
| <p>FWPM_LAYER_OUTBOUND_TRANSPORT_V4</p><p>FWPM_LAYER_OUTBOUND_TRANSPORT_V6</p> | <p>此筛选层位于发送路径中，就在发送的数据包被传递到网络层以进行处理，但在发生任何网络层处理之前。</p><p>此筛选层位于网络层的顶部，而不是位于传输层的底部，以便第三方传输或原始数据包发送的任何数据包都在此层上进行筛选。</p> |
| <p>FWPM_LAYER_OUTBOUND_TRANSPORT_V4_DISCARD</p><p>FWPM_LAYER_OUTBOUND_TRANSPORT_V6_DISCARD</p> | 此筛选层位于发送路径中，用于处理在传输层被丢弃的任何已发送的数据包。 |
| <p>FWPM_LAYER_STREAM_V4</p><p>FWPM_LAYER_STREAM_V6</p> | 此筛选层位于流数据路径中。 此层允许每个流处理网络数据。 在流层，网络数据是双向的。 |
| <p>FWPM_LAYER_STREAM_V4_DISCARD</p><p>FWPM_LAYER_STREAM_V6_DISCARD</p> | 此筛选层保留供将来使用。 |
| <p>FWPM_LAYER_DATAGRAM_DATA_V4</p><p>FWPM_LAYER_DATAGRAM_DATA_V6</p> | 此筛选层位于数据报数据路径中。 此层允许按照每个数据报来处理网络数据。 在数据报层，网络数据是双向的。 |
| <p>FWPM_LAYER_DATAGRAM_DATA_V4_DISCARD</p><p>FWPM_LAYER_DATAGRAM_DATA_V6_DISCARD</p> | 此筛选层位于数据报数据路径中，用于处理任何已丢弃的数据报。 |
| <p>FWPM_LAYER_INBOUND_ICMP_ERROR_V4</p><p>FWPM_LAYER_INBOUND_ICMP_ERROR_V6</p> | 此筛选层位于接收路径中，用于处理传输协议的已接收 ICMP 消息。 |
| <p>FWPM_LAYER_INBOUND_ICMP_ERROR_V4_DISCARD</p><p>FWPM_LAYER_INBOUND_ICMP_ERROR_V6_DISCARD</p> | 此筛选层位于接收路径中，用于处理已被丢弃的已接收 ICMP 消息。 |
| <p>FWPM_LAYER_OUTBOUND_ICMP_ERROR_V4</p><p>FWPM_LAYER_OUTBOUND_ICMP_ERROR_V6</p> | 此筛选层位于用于处理传输协议的已发送 ICMP 消息的发送路径中。 |
| <p>FWPM_LAYER_OUTBOUND_ICMP_ERROR_V4_DISCARD</p><p>FWPM_LAYER_OUTBOUND_ICMP_ERROR_V6_DISCARD</p> | 此筛选层位于发送路径中，用于处理已丢弃的已发送的 ICMP 消息。 |
| <p>FWPM_LAYER_ALE_AUTH_CONNECT_V4</p><p>FWPM_LAYER_ALE_AUTH_CONNECT_V6</p> | 此筛选层允许为传出 TCP 连接授权连接请求，并根据发送的第一个数据包授权传出的非 TCP 流量。 |
| <p>FWPM_LAYER_ALE_AUTH_CONNECT_V4_DISCARD</p><p>FWPM_LAYER_ALE_AUTH_CONNECT_V6_DISCARD</p> | 此筛选层允许处理已丢弃的传出 TCP 连接的连接请求，并为已丢弃的传出非 TCP 流量处理授权。 |
| <p>FWPM_LAYER_ALE_FLOW_ESTABLISHED_V4</p><p>FWPM_LAYER_ALE_FLOW_ESTABLISHED_V6</p> | 如果已建立 TCP 连接，或者未授权 TCP 流量，则可以使用此筛选层通知。 |
| <p>FWPM_LAYER_ALE_FLOW_ESTABLISHED_V4_DISCARD</p><p>FWPM_LAYER_ALE_FLOW_ESTABLISHED_V6_DISCARD</p> | 当已建立的 TCP 连接在流建立的层上被丢弃时，以及在流建立的层上已放弃授权的非 TCP 流量时，此筛选层允许处理。 |
| <p>FWPM_LAYER_ALE_AUTH_LISTEN_V4</p><p>FWPM_LAYER_ALE_AUTH_LISTEN_V6</p> | 此筛选层允许授权 TCP 侦听请求。 |
| <p>FWPM_LAYER_ALE_AUTH_LISTEN_V4_DISCARD</p><p>FWPM_LAYER_ALE_AUTH_LISTEN_V6_DISCARD</p> | 此筛选层允许处理已丢弃的 TCP 侦听请求。 |
| <p>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V4</p><p>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V6</p> | 此筛选层允许向传入的 TCP 连接授权接受请求，并根据收到的第一个数据包授权传入的非 TCP 流量。 |
| <p>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V4_DISCARD</p><p>FWPM_LAYER_ALE_AUTH_RECV_ACCEPT_V6_DISCARD</p> | 此筛选层允许处理已丢弃的传入 TCP 连接的接受请求，以及处理已丢弃的传入非 TCP 流量的授权。 |
| <p>FWPM_LAYER_ALE_AUTH_ROUTE_V4</p><p>FWPM_LAYER_ALE_AUTH_ROUTE_V6</p> | 此筛选层允许检查并筛选 bind 和 connect 请求的路由和路径参数。 |
| <p>FWPM_LAYER_ALE_ENDPOINT_CLOSURE_V4</p><p>FWPM_LAYER_ALE_ENDPOINT_CLOSURE_V6</p> | 此筛选层用于回收 ALE_AUTH_CONNECT 或 ALE_AUTH_RECV_ACCEPT 层中的标注驱动程序所分配的资源。 |
| <p>FWPM_LAYER_ALE_RESOURCE_ASSIGNMENT_V4</p><p>FWPM_LAYER_ALE_RESOURCE_ASSIGNMENT_V6</p> | 此筛选层允许授权传输端口分配、绑定请求、混杂模式请求和 raw 模式请求。 |
| <p>FWPM_LAYER_ALE_RESOURCE_ASSIGNMENT_V4_DISCARD</p><p>FWPM_LAYER_ALE_RESOURCE_ASSIGNMENT_V6_DISCARD</p> | 此筛选层允许处理以下丢弃的项：传输端口分配、绑定请求、混杂模式请求和 raw 模式请求。 |
| <p>FWPM_LAYER_ALE_RESOURCE_RELEASE_V4</p><p>FWPM_LAYER_ALE_RESOURCE_RELEASE_V6</p> | 此筛选层用于回收由任意 ALE_RESOURCE_ASSIGNMENT 层中的标注驱动程序所分配的资源。 |
| <p>FWPM_LAYER_IPSEC_KM_DEMUX_V4</p><p>FWPM_LAYER_IPSEC_KM_DEMUX_V6</p> | 此筛选层用于确定本地系统为发起方时要调用的密钥模块。 这是用户模式筛选层。 |
| <p>FWPM_LAYER_IPSEC_V4</p><p>FWPM_LAYER_IPSEC_V6</p> | 此筛选层允许键控模块在协商快速模式安全关联时查找快速模式策略信息。 这是用户模式筛选层。 |
| <p>FWPM_LAYER_IKEEXT_V4</p><p>FWPM_LAYER_IKEEXT_V6</p> | 在协商主模式安全关联时，此筛选层允许 IKE 和经过身份验证的 IP 模块查找主模式策略信息。 这是用户模式筛选层。 |
| FWPM_LAYER_RPC_UM | 此筛选层允许检查用户模式下提供的 RPC 数据字段。 这是用户模式筛选层。 |
| FWPM_LAYER_RPC_EPMAP | 此筛选层允许检查终结点解析期间用户模式下可用的 RPC 数据字段。 这是用户模式筛选层。 |
| FWPM_LAYER_RPC_EP_ADD | 此筛选层允许在添加新的终结点时检查用户模式下可用的 RPC 数据字段。 这是用户模式筛选层。 |
| FWPM_LAYER_RPC_PROXY_CONN | 此筛选层允许检查 RpcProxy 连接请求。 这是用户模式筛选层。 |
| FWPM_LAYER_RPC_PROXY_IF | 此筛选层允许检查用于 RpcProxy 连接的接口。 这是用户模式筛选层。 |
| FWPM_LAYER_INBOUND_MAC_FRAME_ETHERNET | 此筛选层允许将入站下限 (的 MAC 帧数据检查到 NDIS 协议驱动程序) 层。 **注意**：仅在 Windows 8 和更高版本上可用。 |
| FWPM_LAYER_OUTBOUND_MAC_FRAME_ETHERNET | 此筛选层允许将出站上限 (的 MAC 帧数据检查到 NDIS 协议驱动程序) 层。 **注意**：仅在 Windows 8 和更高版本上可用。 |
| FWPM_LAYER_INBOUND_MAC_FRAME_NATIVE | 此筛选层允许将入站下限 (的 MAC 帧数据检查到 NDIS 微型端口驱动程序) 层。 **注意**：仅在 Windows 8 和更高版本上可用。 |
| FWPM_LAYER_OUTBOUND_MAC_FRAME_NATIVE | 此筛选层允许将出站下 (的 MAC 帧数据检查到 NDIS 微型端口驱动程序) 层。 **注意**：仅在 Windows 8 和更高版本上可用。 |
| FWPM_LAYER_INGRESS_VSWITCH_ETHERNET | 此筛选层允许检查 Hyper-v 可扩展交换机的入口802.3 数据。 **注意**：仅在 Windows 8 和更高版本上可用。 |
| FWPM_LAYER_EGRESS_VSWITCH_ETHERNET | 此筛选层允许检查 Hyper-v 可扩展交换机的出口802.3 数据。 **注意**：仅在 Windows 8 和更高版本上可用。 |
| <p>FWPM_LAYER_INGRESS_VSWITCH_TRANSPORT_V4</p><p>FWPM_LAYER_INGRESS_VSWITCH_TRANSPORT_V6</p> | 此筛选层允许检查 Hyper-v 可扩展交换机的入口传输数据。 **注意**：仅在 Windows 8 和更高版本上可用。 |
| <p>FWPM_LAYER_EGRESS_VSWITCH_TRANSPORT_V4</p><p>FWPM_LAYER_EGRESS_VSWITCH_TRANSPORT_V6</p> | 此筛选层允许检查 Hyper-v 可扩展交换机的出口传输数据。 **注意**：仅在 Windows 8 和更高版本上可用。 |

