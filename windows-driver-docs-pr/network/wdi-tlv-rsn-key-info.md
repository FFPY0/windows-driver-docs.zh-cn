---
title: WDI_TLV_RSN_KEY_INFO
description: WDI_TLV_RSN_KEY_INFO 是包含 Rsn Eapol 密钥参数的 TLV。
ms.date: 04/02/2018
keywords:
- 从 Windows Vista 开始 WDI_TLV_RSN_KEY_INFO 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: da2eec129112c745739c50ced7f7b825690c687b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96834245"
---
# <a name="wdi_tlv_rsn_key_info"></a>WDI_TLV_RSN_KEY_INFO

WDI_TLV_RSN_KEY_INFO 是包含 Rsn Eapol 密钥参数的 TLV。 此 TLV 是 [WDI_TLV_PM_PROTOCOL_OFFLOAD_80211RSN_REKEY](wdi-tlv-pm-protocol-offload-80211rsn-rekey.md) tlv 的值。

## <a name="tlv-type"></a>TLV 类型

0x148

## <a name="length"></a>长度

以下值的大小 (以字节为单位) 。

## <a name="values"></a>值

| 类型 | 描述 |
| --- | --- |
| UINT32 | 指定协议卸载 ID 的 UINT32 值。 这是操作系统提供的用于标识卸载协议的值。 在 OS 向下发送添加请求或完成对过量驱动程序的请求之前，操作系统会将 ProtocolOffloadId 设置为在网络适配器上的协议卸载之间唯一的值。 |
| UINT64 | 指定重播计数器的 UINT64 值。 |
| UINT8 \[ 16\] | 指定 IEEE 802.11 密钥确认密钥 (KCK) 的 UINT8 数组。 |
| UINT8 \[ 16\] | 指定 IEEE 802.11 密钥加密密钥 (KEK) 的 UINT8 数组。  |
 

## <a name="requirements"></a>要求

**支持的最低客户端**： Windows 10，版本1803

**支持的最低服务器**： Windows server 2016

**标头**： Wditypes. hpp

