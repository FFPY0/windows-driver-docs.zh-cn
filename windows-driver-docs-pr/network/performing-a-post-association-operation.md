---
title: 执行关联后的操作
description: 执行关联后的操作
keywords:
- 后关联操作 WDK 本机 802.11 IHV 扩展 DLL
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 25ebcc6a20163216516490627f45198dfa186c60
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839455"
---
# <a name="performing-a-post-association-operation"></a>执行关联后的操作




 

当无线 LAN (WLAN) 适配器使用接入点 (AP) 成功完成802.11 关联操作时，本机802.11 微型端口驱动程序会通过使 [NDIS \_ 状态 \_ DOT11 \_ 关联 \_ 完成](/previous-versions/windows/hardware/wireless/ndis-status-dot11-association-completion) 指示来通知操作系统。 有关关联操作的详细信息，请参阅 [关联运算](/previous-versions/windows/hardware/wireless/association-operations)。

**注意**  对于 Windows Vista，IHV 扩展 DLL 仅支持基础结构基本服务集 (BSS) 网络。

 

操作系统收到 NDIS \_ 状态 \_ DOT11 \_ 关联 \_ 完成指示后，它会调用 [*Dot11ExtIhvPerformPostAssociate*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate) 函数来通知 IHV 扩展 DLL 以下内容：

-   为与 AP 关联而创建新的数据端口。 通过 [*Dot11ExtIhvPerformPostAssociate*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate)函数的 *PPORTSTATE* 参数向 IHV 扩展 DLL 传递数据端口的当前状态。 有关端口状态参数的详细信息，请参阅 [**DOT11 \_ 端口 \_ 状态**](/windows-hardware/drivers/ddi/wlclient/ns-wlclient-_dot11_port_state)。

-   无线 LAN (WLAN) 适配器与 AP 之间的关联参数。 通过 [*Dot11ExtIhvPerformPostAssociate*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate)函数的 *PDOT11ASSOCPARAMS* 参数向 IHV 扩展 DLL 传递关联参数。 有关关联参数的详细信息，请参阅 [**DOT11 \_ association \_ 完成 \_ 参数**](/windows-hardware/drivers/ddi/windot11/ns-windot11-dot11_association_completion_parameters)。

调用 [*Dot11ExtIhvPerformPostAssociate*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate) 时，IHV 扩展 DLL 使用 AP 启动关联后操作以对数据端口进行身份验证。 完成此操作后，IHV 扩展 DLL 可以执行以下操作：

-   为新的数据端口分配所需的任何资源。

-   针对关联的数据端口执行专有安全处理。 IHV 扩展 DLL 可从 [*Dot11ExtIhvPerformPostAssociate*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate)函数的 *pPortState* 参数确定数据端口的当前状态。

-   调用 [**Dot11ExtSendUIRequest**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_ui_request) 函数以请求 IHV UI 扩展 DLL 提示用户输入安全参数，如用户的凭据。

-   使用通过 [**Dot11ExtSetAuthAlgorithm**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_auth_algorithm)启用的身份验证算法向 AP 进行身份验证。 IHV 扩展 DLL 在预关联操作过程中调用 **Dot11ExtSetAuthAlgorithm** 。 有关此操作的详细信息，请参阅 [预关联操作](pre-association-operations.md)。

-   通过调用 [**Dot11ExtSendPacket**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_packet) 函数将安全数据包发送到 AP。

    发送安全数据包后，操作将通过调用 [*Dot11ExtIhvSendPacketCompletion*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_send_packet_completion) 函数通知 IHV 扩展 DLL。

    有关发送安全数据包的详细信息，请参阅 [发送操作](send-operations.md)。

-   从 AP 接收安全数据包。 操作系统为 WLAN 适配器接收的每个安全数据包调用 [*Dot11ExtIhvReceivePacket*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_receive_packet) 函数。

    每个接收到的安全数据包都按从 WLAN 适配器接收到的顺序进行序列化和指示。 操作系统只调用 [*Dot11ExtIhvReceivePacket*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_receive_packet) 函数来指示接收到的安全数据包，这些数据包与 IEEE EtherTypes 列表中的条目相匹配，后者由 IHV 扩展 DLL 通过调用 [**Dot11ExtSetEtherTypeHandling**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_ethertype_handling) 函数指定。

    有关接收安全数据包的详细信息，请参阅 [接收操作](receive-operations.md)。

-   使用通过身份验证算法派生的密码密钥配置 WLAN 适配器。 可以调用以下 IHV 扩展性函数，将密码密钥下载到 WLAN 适配器。
    -   [**Dot11ExtSetDefaultKey**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_default_key)
    -   [**Dot11ExtSetDefaultKeyId**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_default_key_id)
    -   [**Dot11ExtSetKeyMappingKey**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_key_mapping_key)
-   配置 WLAN 适配器，以通过调用 [**Dot11ExtSetExcludeUnencrypted**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_set_exclude_unencrypted) IHV 扩展性函数排除未加密的数据包。

对数据端口进行身份验证后，必须调用 [**Dot11ExtPostAssociateCompletion**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_post_associate_completion) 来完成关联后操作。

下图显示了在之后的关联操作过程中所涉及的步骤。

![说明在后期关联操作过程中涉及的步骤的关系图](images/ihv-ext-postassoc.png)

执行后关联操作时，IHV 扩展 DLL 必须遵循这些准则。

-   IHV 扩展 DLL 必须从对 [*Dot11ExtIhvPerformPostAssociate*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_perform_post_associate)的调用异步调用 [**Dot11ExtPostAssociateCompletion**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_post_associate_completion) 。

-   完成后关联操作后，每当数据端口的身份验证状态发生更改时，IHV 扩展 DLL 都可以调用 [**Dot11ExtPostAssociateCompletion**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_post_associate_completion) 。

-   如果调用 [*Dot11ExtIhvAdapterReset*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_adapter_reset) 函数，则 IHV 扩展 DLL 必须通过调用 [**Dot11ExtPostAssociateCompletion**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_post_associate_completion)取消所有挂起的后关联操作。 有关重置操作的详细信息，请参阅 [802.11 WLAN 适配器重置](802-11-wlan-adapter-reset.md)。

-   如果调用 [*Dot11ExtIhvDeinitAdapter*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_deinit_adapter) 函数，则 IHV 扩展 DLL 必须在内部取消所有挂起的关联后操作。 但是，它不能调用任何只能在适配器初始化之后调用的 IHV 扩展性函数，包括 [**Dot11ExtPostAssociateCompletion**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_post_associate_completion)。 有关 IHV 扩展性函数的详细信息，请参阅 [本机 802.11 IHV 扩展性函数](./native-802-11-ihv-extensibility-functions.md)。

 

 
