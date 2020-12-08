---
title: CM_PROB_HELD_FOR_EJECT
description: CM_PROB_HELD_FOR_EJECT
keywords:
- CM_PROB_HELD_FOR_EJECT
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d6c43a1e21d87b0bf9e314901d3174852412e0ba
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783123"
---
# <a name="code-47---cm_prob_held_for_eject"></a>代码 47 - CM_PROB_HELD_FOR_EJECT

此设备管理器错误消息指示设备已准备好进行弹出。

## <a name="error-code"></a>错误代码

47

### <a name="display-message"></a>显示消息

"Windows 无法使用此硬件设备，因为它已为" 安全删除 "做好准备，但尚未从计算机中删除它。  (代码 47) "

"若要解决此问题，请将此设备从计算机中拔出，然后再次插上。"

### <a name="recommended-resolution"></a>推荐的解决方案

拔出设备并重新插入。 或者，选择 " **重新启动计算机** " 将重新启动计算机并使设备可用。

此错误仅在以下情况下发生：用户调用热插拔程序来准备要删除的设备 (该设备调用 [**CM_Request_Device_Eject**](/windows/win32/api/cfgmgr32/nf-cfgmgr32-cm_request_device_ejectw)) ，或者，如果用户按 (调用 [**IoRequestDeviceEject**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iorequestdeviceeject)) 的物理弹出按钮。 用户可以准备当前不可删除的设备，例如，光盘在便携式计算机和扩展坞托盘之间补漏白。
