---
title: 在气球通知中显示自定义 UI 页
description: 在气球通知中显示自定义 UI 页
keywords:
- 自定义 UI WDK 本机 802.11 IHV UI 扩展 DLL、气球通知
- 气球通知 WDK
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 888181918fd9191295abff569bdd65ff30fe4bfb
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838757"
---
# <a name="displaying-custom-ui-pages-within-a-balloon-notification"></a>在气球通知中显示自定义 UI 页




 

如果本机 802.11 IHV 扩展 DLL 调用 [**Dot11ExtSendUIRequest**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_ui_request) 来 (UI) 显示自定义用户界面，则当无线 LAN (WLAN) 适配器连接到无线网络时，操作系统将通过可单击的气球通知显示 UI。 在这种情况下，自定义 UI 的请求显示为气球通知：

-   在本机 802.11 IHV 扩展 DLL 调用 [**Dot11ExtPostAssociateCompletion**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_post_associate_completion) ，以成功完成关联后操作。

-   在操作系统调用 DLL 的 [*Dot11ExtIhvAdapterReset*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_adapter_reset) IHV 处理程序函数来重置 WLAN 连接之前。

有关本机 802.11 IHV 扩展 DLL 如何请求显示自定义 UI 的详细信息，请参阅 [请求显示自定义 ui](requesting-the-display-of-a-custom-ui.md)。

当处理自定义 UI 请求作为气球通知时，操作系统将执行以下操作。

1.  调用本机 802.11 IHV 扩展 DLL 的 [*Dot11ExtIhvIsUIRequestPending*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_is_ui_request_pending) IHV 处理程序函数来确定 UI 请求是否仍处于挂起状态。 操作系统使用由本机 802.11 IHV 扩展 DLL 传递到 [**Dot11ExtSendUIRequest**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_ui_request) 的全局唯一标识符 (GUID) 来指定 UI 请求。

2.  如果对于指定的 UI 请求， [*Dot11ExtIhvIsUIRequestPending*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_is_ui_request_pending) 返回 **TRUE** ，则操作系统将调用本机 802.11 IHV UI 扩展 DLL 的 [**IDot11ExtUI：： GetDot11ExtUIBalloonText**](/previous-versions/windows/hardware/wireless/ff553771(v=vs.85)) 方法。 通过此方法，DLL 返回一个字符串缓冲区，其中包含要在气球状通知中显示的本地化文本。

3.  显示包含本地化文本的气球通知。

4.  如果最终用户单击了气球通知，则操作系统将启动请求的 **IWizardExtension** COM 接口支持的自定义 UI。 调用 [**Dot11ExtSendUIRequest**](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11ext_send_ui_request)时，NATIVE 802.11 IHV extension dll 会在本机 802.11 IHV UI 扩展 dll 中指定 **IWIZARDEXTENSION** 实现 (CLSID) 的类标识符。

    当操作系统调用 **IWizardExtension：： AddPages** 方法时，本机 802.11 IHV UI 扩展 DLL 返回表示自定义 UI 页面的 PROPSHEETPAGE 结构的句柄数组。

    有关 **IWizardExtension** com 接口的详细信息，请参阅 [IWizardExtension com interface](/windows/win32/api/shobjidl/nn-shobjidl-iwizardextension)。 有关 PROPSHEETPAGE 结构的详细信息，请参阅 Microsoft Windows SDK 中的文档。

5.  通过 **IWizardSite** COM 接口，按本机 802.11 IHV UI 扩展 DLL 指定的方式浏览 UI 页。 有关此接口的详细信息，请参阅 [IWIZARDSITE COM interface](/windows/win32/api/shobjidl/nn-shobjidl-iwizardsite)。

显示自定义 UI 时，本机 802.11 IHV UI 扩展 DLL 可以通过 [IPROPERTYBAG COM 接口](/previous-versions/windows/internet-explorer/ie-developer/platform-apis/aa768196(v=vs.85))读取或写入特定于上下文的数据。 有关此过程的详细信息，请参阅 [访问配置文件和上下文数据](accessing-profile-and-context-data.md)。 自定义 UI 的显示完成后，本机 802.11 IHV UI 扩展 DLL 可通过调用 **WlanSendUIResponse** 将用户输入的响应数据返回到本机 802.11 IHV 扩展 dll。 DLL 传入 UI 请求的 GUID，以及指向包含响应数据的缓冲区的指针。

在本机 802.11 IHV UI 扩展 DLLcalls **WlanSendUIResponse** 后，操作系统将调用本机 802.11 IHV 扩展 DLL 的 [*Dot11ExtIhvProcessUIResponse*](/windows-hardware/drivers/ddi/wlanihv/nc-wlanihv-dot11extihv_process_ui_response) IHV 处理程序函数来转发自定义 UI 的响应数据。

有关 **WlanSendUIResponse** API 的详细信息，请参阅 Windows SDK 中的文档。

 

 
