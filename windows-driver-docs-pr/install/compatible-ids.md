---
title: 兼容 ID
description: 兼容 ID 是供应商定义的标识字符串，Windows 使用它将设备与 INF 文件匹配。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3710190fbb286f8ae5b6b8fea529f25d63d18133
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782979"
---
# <a name="compatible-id"></a>兼容 ID

兼容 ID 是供应商定义的标识字符串，Windows 使用它将设备与 INF 文件匹配。 设备可以与兼容 Id 列表相关联。 应按照降低适用性顺序列出兼容 Id。 如果 Windows 找不到与某个设备的硬件 Id 相匹配的 INF 文件，它将使用兼容 Id 查找 INF 文件。 兼容 Id 与 [硬件 id](hardware-ids.md)的格式相同。 但是，兼容 Id 通常比硬件 Id 更通用。

如果供应商提供指定驱动程序节点的兼容 ID 的 INF 文件，则供应商应确保其 INF 文件可以支持与兼容 ID 匹配的所有硬件。

若要获取设备的兼容 Id 列表，请调用 [**IoGetDeviceProperty**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iogetdeviceproperty) ，并将 *DeviceProperty* 参数设置为 **DevicePropertyCompatibleID**。 此例程检索到的兼容 Id 列表是 [REG_MULTI_SZ](/windows/desktop/SysInfo/registry-value-types) 值。 兼容 ID 列表中的最大字符数（包括每个兼容 ID 和最终 NULL 终止符后的 NULL 终止符） REGSTR_VAL_MAX_HCID_LEN。 兼容 Id 列表中可能的最大 Id 数为64。
