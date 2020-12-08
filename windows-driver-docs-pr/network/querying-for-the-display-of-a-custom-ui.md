---
title: 查询自定义 UI 的显示
description: 查询自定义 UI 的显示
keywords:
- 自定义 UI WDK 本机 802.11 IHV UI 扩展 DLL，查询
- 查询自定义 UI 显示
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17cb6105e5f154e7430f5feeebea1b6dbe2eb94f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793387"
---
# <a name="querying-for-the-display-of-a-custom-ui"></a>查询自定义 UI 的显示




 

操作系统可以查询本机 802.11 IHV 扩展 DLL，以确定 DLL 是否有要显示的自定义 UI。 每当无线 LAN (WLAN) 适配器转换为 WLAN 网络连接过程中的以下阶段之一时，操作系统就会查询 DLL。

<a href="" id="pre-association-------"></a>**预先关联**   
IHV 扩展 DLL 启动前关联操作之前的连接阶段。 有关预关联操作的详细信息，请参阅 [预关联](pre-association-operations.md)操作。

<a href="" id="post-association-------"></a>**后关联**   
IHV 扩展 DLL 完成后关联操作的连接阶段。 有关后处理后操作的详细信息，请参阅 [之后的关联操作](post-association-operations.md)。

操作系统调用本机 802.11 IHV 扩展 DLL 的 [*Dot11ExtIhvQueryUIRequest*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_query_ui_request) IHV 处理程序函数来查询是否可以显示自定义 UI。 操作系统通过 *connectionPhase* 参数传递连接进程的当前阶段。 如果必须显示自定义 UI，则 DLL 通过 p *pIhvUIRequest* 参数返回 [**DOT11EXT \_ IHV \_ UI \_ 请求**](/windows-hardware/drivers/ddi/wlanihv/ns-wlanihv-_dot11ext_ihv_ui_request)结构。

通过 [**DOT11EXT \_ IHV \_ UI \_ 请求**](/windows-hardware/drivers/ddi/wlanihv/ns-wlanihv-_dot11ext_ihv_ui_request) 结构，本机 802.11 ihv 扩展 DLL 通过以下数据指定自定义 UI。

-   用户会话标识符 (ID) ，用于标识特定用户上下文。

-   全局唯一 ID (GUID) ，用于标识特定 UI 请求。

-   类 ID (在本机 802.11 IHV UI 扩展 DLL 中实现的 **IWizardExtension** COM 接口的 CLSID) 。 CLSID 用于请求 DLL 支持的特定自定义 UI。

    有关 **IWizardExtension** com 接口的详细信息，请参阅 [IWizardExtension com interface](/windows/win32/api/shobjidl/nn-shobjidl-iwizardextension)。

-   包含由独立硬件供应商 (IHV 定义的专有格式的数据的缓冲区) 并由指定的 **IWizardExtension** COM 接口处理。 例如，缓冲区可能包含自定义 UI 中显示的默认值。

自定义 UI 将在标准网络连接 UI 中显示为一组向导页面。 有关此过程的详细信息，请参阅在 [网络连接向导中显示自定义 UI 页面](displaying-custom-ui-pages-within-the-network-connection-wizard.md)。

 

 
