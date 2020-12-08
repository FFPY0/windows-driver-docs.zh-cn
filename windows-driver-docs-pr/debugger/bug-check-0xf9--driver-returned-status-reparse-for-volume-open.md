---
title: Bug 检查 0xF9 DRIVER_RETURNED_STATUS_REPARSE_FOR_VOLUME_OPEN
description: DRIVER_RETURNED_STATUS_REPARSE_FOR_VOLUME_OPEN bug 检查，它指示驱动程序返回的 STATUS_REPARSE 到 IRP_MJ_CREATE 请求，但没有尾随名称。
keywords:
- Bug 检查 0xF9 DRIVER_RETURNED_STATUS_REPARSE_FOR_VOLUME_OPEN
- DRIVER_RETURNED_STATUS_REPARSE_FOR_VOLUME_OPEN
ms.date: 07/21/2020
topic_type:
- apiref
api_name:
- DRIVER_RETURNED_STATUS_REPARSE_FOR_VOLUME_OPEN
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f62f4f7386b7055e09f7406a2a6fd707c91b1501
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819239"
---
# <a name="bug-check-0xf9-driver_returned_status_reparse_for_volume_open"></a>Bug 检查0xF9：驱动 \_ 程序 \_ 返回 \_ \_ 的 \_ 卷 \_ 打开状态重新分析

驱动程序 \_ 返回了 " \_ \_ \_ \_ 卷 \_ 打开 bug 检查的状态重新分析" 的值为 "0x000000F9"。 这表明驱动程序将状态重新 \_ 分析返回给 IRP \_ MJ \_ CREATE 请求，但没有尾随名称。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="driver_returned_status_reparse_for_volume_open-parameters"></a>驱动 \_ 程序 \_ 返回 \_ \_ \_ 卷 \_ 开放参数的状态重新分析

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>已打开的设备对象</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>向其发出 IRP_MJ_CREATE 请求的设备对象</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>包含要被重新分析的 (文件的新名称的 Unicode 字符串的地址) </p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>驱动程序为 IRP_MJ_CREATE 请求返回的信息</p></td>
</tr>
</tbody>
</table>

## <a name="remarks"></a>备注

[**！分析**](-analyze.md)调试扩展显示有关 bug 检查的信息，可帮助确定根本原因。

\_仅应为 IRP \_ MJ \_ CREATE requests 返回带有尾随名称的状态重新分析，因为该驱动程序支持名称空间。 

有关使用文件系统驱动程序的详细信息，请参阅 [文件系统驱动程序设计指南](../ifs/index.md)。 有关 IRP \_ MJ 创建请求的信息， \_ 请参阅 [IRP_MJ_CREATE (IFS) ](../ifs/irp-mj-create.md)。
