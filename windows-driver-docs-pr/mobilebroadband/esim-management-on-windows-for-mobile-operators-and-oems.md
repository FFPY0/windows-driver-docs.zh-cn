---
title: 用于移动运营商和 OEM 的 Windows 上的 eSIM 卡管理
description: 用于移动运营商和 OEM 的 Windows 上的 eSIM 卡管理
ms.date: 05/23/2019
ms.localizationpriority: medium
ms.openlocfilehash: 56c0bd6c353e9c4926d0a4dea3aa8b8e603f1025
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788539"
---
# <a name="esim-management-on-windows-for-mobile-operators-and-oems"></a>用于移动运营商和 OEM 的 Windows 上的 eSIM 卡管理

## <a name="mobile-operators-and-oems"></a>移动运营商和 Oem

如果你是移动运营商或 OEM，并且想要在 Windows 上支持 eSIM 管理，请执行以下步骤：

1.  (HLK) 测试运行中执行硬件实验室工具包。 这可确保与 Windows 10 eSIM 支持的调制解调器硬件兼容性。 Oem 和 Odm 必须确保执行以下的 HLK eSIM 测试：
    1. 基本 eSIM 支持测试用例：
        - [Win6_4.MB.CDMA.Data.TestLowLevelUiccAccess](/windows-hardware/test/hlk/testref/f27c8d81-7e2b-49d1-be4c-614bf62f003c)
        - [Win6_4.MB.GSM.Data.TestLowLevelUiccAccess](/windows-hardware/test/hlk/testref/104db926-5cc4-47ad-a7d0-ff476b0f57a1)
    2. 对于具有可移动 SIM 槽和焊料 eUICC 的 Windows 10 设备：
        - [WIN6_4 MB。CDMA.TestSlot](/windows-hardware/test/hlk/testref/049a0532-3d58-49aa-ac3d-2a9b8aab24a7) 和/或 [WIN6_4. MB。GSM.Data. TestSlot](/windows-hardware/test/hlk/testref/defddebe-cc40-4d6f-9b0c-ca5ca9a1cb4d)
        - [WIN6_4 MB。CDMA.TestDeviceCapsEx](/windows-hardware/test/hlk/testref/e4ec5199-0841-4864-ac17-b6b71f81cdf3) 和/或 [WIN6_4. MB。GSM.Data. TestDeviceCapsEx](/windows-hardware/test/hlk/testref/75c812d5-8c7d-4589-8336-7d72f2feb987)

Windows 提供了移动设备管理提供程序在企业用例中管理 eSIM 配置文件的功能。 但是，Windows 不会限制生态系统伙伴如何向其自己的合作伙伴和/或客户提供此功能。 因此，可以通过与 Windows OMA 集成来支持 eSIM 配置文件管理功能。 这样，便可以根据公司政策远程管理 eSIM 配置文件。

如果只想集成并使用一个 MDM 提供程序，请直接联系该访问接口。 如果你想要使用不同的 MDM 提供程序向客户提供 eSIM 管理，请与 orchestrator 提供商联系。 Orchestrator 提供程序充当用于处理 MDM 载入和移动运营商载入的代理。 它们的作用是使所有参与方的过程尽可能顺利且可缩放。 可以联系的潜在 orchestrator 提供程序包括：
* [HPE 的设备权利网关](https://www.hpe.com/emea_europe/en/solutions/digital-communications-services.html)
* [IDEMIA 的智能连接集线器](https://www.idemia.com/smart-connect-hub)

## <a name="esim-management-for-other-audiences"></a>其他受众的 eSIM 管理

如果你是 MDM 提供商，并且想要在 Windows 上支持 eSIM 管理，请参阅 [移动设备管理提供商如何支持 windows 上的 Esim 管理](/windows/client-management/mdm/esim-enterprise-management)。

如果你是组织中的最终用户，并且想要为组织提供的设备上的手机网络数据连接使用 eSIM，请参阅 [在 Windows 10 电脑上使用 esim 获取手机网络数据连接](https://support.microsoft.com/help/4020763/windows-10-use-esim-for-cellular-data)。
