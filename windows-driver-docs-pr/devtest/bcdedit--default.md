---
title: BCDEdit/默认27000
description: '**BCDEdit/默认 27000** 命令将设置启动管理器在超时过期时将使用的默认条目。'
ms.date: 09/23/2020
keywords:
- BCDEdit/默认27000驱动程序开发工具
topic_type:
- apiref
api_name:
- BCDEdit /default
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 73ae3ff18de911ea9b71d82780d20e62ffd42ee2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822589"
---
<a name="bcdedit-default"></a>BCDEdit/默认27000
============

**BCDEdit/默认 27000** 命令将设置启动管理器在超时过期时将使用的默认条目。

``` syntax
bcdedit /default <id>
```

> [!NOTE]
> 设置 BCDEdit 选项之前，可能需要禁用或暂停计算机上的 BitLocker 和安全启动。

## <a name="parameters"></a>参数

**\<id\>**

指定在超时过期时要用作默认值的启动项的标识符。 有关标识符的详细信息，请运行 "bcdedit/？ ID "。

## <a name="examples"></a>示例

以下命令将指定项设置为默认启动管理器项。

`bcdedit /default {cbd971bf-b7b8-4885-951a-fa03044f5d71}`

以下命令将基于 NTLDR 的 OS 加载程序设置为默认条目：

`bcdedit /default {ntldr}`
